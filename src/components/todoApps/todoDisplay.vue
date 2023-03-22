<script setup>
import ItemsComp from "./ItemsComp.vue";
import { ref, watch, onMounted} from "vue";
import { defineProps } from "vue";

const todoItems = ref("");
let change = ref(false);

defineProps(["Theme", "toogleThemes"]);

const todos = ref([]);

const alltodos = ref([
  {
    id: 0,
    name: "Jungle Around the park 3X",
    completed: false,
    onMouseEnter: false,
    list: 1,
  },
  {
    id: 1,
    name: "10 minute meditation",
    completed: false,
    onMouseEnter: false,
    list: 1,
  },
  {
    id: 2,
    name: "Read for 1 hour",
    completed: false,
    onMouseEnter: false,
    list: 1,
  },
  {
    id: 3,
    name: "Pick up groceries",
    completed: false,
    onMouseEnter: false,
    list: 1,
  },
]);

const addTodo = () => {
  alltodos.value.push({
    id: alltodos.value.length + 1,
    name: todoItems.value,
    completed: false,
    onMouseEnter: false,
    list: 1,
  });
  todoItems.value = "";
  change = false;
};

const removeTodo = (id) => {
  alltodos.value = alltodos.value.filter(function (todo) {
    return todo.id !== id;
  });
  todos.value = alltodos.value;
};

watch(
  alltodos,
  (newVal) => {
    localStorage.setItem("alltodos", JSON.stringify(newVal));
  },
  { deep: true }
);

onMounted(() => {

  console.log('mounted')
  // if (window.localStorage.length===0) {
    console.log("yes");
    localStorage.setItem("alltodos", JSON.stringify(alltodos.value));
    
  // } else {
    alltodos.value = JSON.parse(localStorage.getItem("alltodos")) || [];
    todos.value = alltodos.value;
  // }
});



const removeCompleted = () => {
  alltodos.value = alltodos.value.filter(function (each) {
    return each.completed !== true;
  });
  todos.value = alltodos.value;
};

const showCompleted = () => {
  todos.value = alltodos.value.filter(function (each) {
    return each.completed == true;
  });
};

const showActive = () => {
  todos.value = alltodos.value.filter(function (each) {
    return each.completed == false;
  });
};

const showAll = () => {
  todos.value = alltodos.value;
};

const drop = (e) => {
  const itemId = e.dataTransfer.getData("itemId");
  // const item = this.todos.filter((todo)=>{todo.id==itemId})
  const item = document.getElementById(itemId);

  e.target.appendChild(item);
};
</script>

<template>
  <section class="todo-display">
    <div
      class="input-wrap"
      :class="
        toogleThemes ? Theme.darkTheme.inputDark : Theme.lightTheme.inputLight
      "
    >
      <p></p>
      <input
        v-model="todoItems"
        class="input"
        type="text"
        placeholder="Create a new todo..."
        @keyup.enter="addTodo()"
        @click="change = true"
        @mouseleave="
          () => {
            if (todoItems === '') {
              return;
            }
            if (change == true) {
              addTodo();
              focus = false;
            }
          }
        "
      />
    </div>
    <main
      class="main"
      :class="
        toogleThemes
          ? Theme.darkTheme.todoDisplaydarkMain
          : Theme.lightTheme.todoDisplayLightMain
      "
    >
      <div class="todo-display-items" @dragover.prevent @drop.prevent="drop">
        <ItemsComp :todos="todos" @removeTodo="removeTodo" />
      </div>

      <!--                       mobile view  start-->
      <div class="mobile-view">
        <p class="item-info">{{ todos.length }} items left</p>
        <button
          class="btn"
          :class="
            toogleThemes
              ? Theme.darkTheme.completedDark
              : Theme.lightTheme.completedLight
          "
          @click="removeCompleted()"
        >
          Clear completed
        </button>
      </div>
      <!--                             mobile view   end           -->
    </main>

    <div
      class="tool-box"
      :class="
        toogleThemes
          ? Theme.darkTheme.todoDisplayDarkToolBox
          : Theme.lightTheme.todoDisplayLightToolBox
      "
    >
      <p class="item-info item-info-no-display">
        {{ todos.length }} items left
      </p>

      <button class="btn all" @click="showAll()">All</button>

      <button
        class="btn"
        :class="
          toogleThemes
            ? Theme.darkTheme.activeDark
            : Theme.lightTheme.activeLight
        "
        @click="showActive"
      >
        Active
      </button>

      <button
        class="btn hover"
        :class="
          toogleThemes
            ? Theme.darkTheme.completedDark
            : Theme.lightTheme.completedLight
        "
        @click="showCompleted()"
      >
        Completed
      </button>

      <button
        class="btn item-info-no-display hover"
        :class="
          toogleThemes
            ? Theme.darkTheme.completedDark
            : Theme.lightTheme.completedLight
        "
        @click="removeCompleted()"
      >
        Clear completed
      </button>
    </div>
  </section>
</template>

<style scoped>
@font-face {
  font-family: "Josefin_Sans";
  src: url("@/assets/Josefin_Sans/static/JosefinSans-Regular.ttf");
}
html {
  padding: 0;
  margin: 0;
  font-family: "Josefin_Sans";
  font-weight: 100;
 
}
.main {
  background-color: blueviolet;
  padding-bottom: 5px;
  border-top-left-radius: 6px;
  border-top-right-radius: 6px;
  gap: 15px;

}

.todo-display {
  display: flex;
  flex-direction: column;
  margin: 0 auto;
  width: 40%;
  border-radius: 10px;
  /* border: 2px solid red; */
}

.mobile-view {
  display: none;
}

.input-wrap {
  display: flex;
  margin: 0 auto;
  width: 100%;
  border-radius: 6px;
  padding-left: 20px;
  align-items: center;
  /* border: solid red; */
  margin-bottom: 20px;
}

.input {
  height: 50px;
  color: inherit;
  background-color: inherit;
  border-radius: 10px;
  /* padding: 20px; */
  margin-left: 20px;
  outline: none;
  border-width: 0;
  font-family: "Josefin_Sans";
}
.input-wrap p {
  border: 1px solid grey;
  width: 30px;
  height: 30px;
  border-radius: 50%;
}
.tool-box {
  display: flex;
  padding-left: 20px;
  padding-right: 20px;
  border-end-start-radius: 5px;
  border-bottom-right-radius: 5px;
  font-family: "Josefin_Sans";
}
.item-info {
  font-size: 0.9em;
}
.btn {
  background-color: inherit;
  outline: none;
  border-width: 0;
  margin-left: auto;
  color: inherit;
  font-family: "Josefin_Sans";
}
.btn:hover {
  cursor: pointer;
}
.all {
  color: blue;
}

.completed-dark:hover {
  color: white;
}
.completed-light:hover {
  color: black;
}
.todo-display-dark-main {
  background-color: var(--DarkDesaturatedBlue);
  color: var(--LightGrayishBlue);
  box-shadow: 5px 8px 20px 1px var(--DarkBlue);
}
.todo-display-dark-tool-box {
  background-color: var(--DarkDesaturatedBlue);
  color: var(--DarkGrayishBlue);
  /* border: solid; */
}
.todo-display-light-main {
  background-color: white;
  box-shadow: 5px 8px 20px 1px rgb(189, 187, 187);
}
.todo-display-light-tool-box {
  background-color: white;
  color: var(--DarkGrayishBlue);
  box-shadow: 5px 8px 20px 1px rgb(189, 187, 187);
}
.input-dark {
  background-color: var(--DarkBlue);
  color: var(--DarkGrayishBlue);
}
.input-light {
  background-color: white;
}
.active-dark:hover {
  color: white;
}
.active-light:hover {
  color: var(--DarkBlue);
}

@media screen And (min-width: 180px) And (max-width: 767px) {
  .main {
    /* border: solid red; */
    border-radius: 6px;
    padding-bottom: 5px;
  }

  .todo-display-dark-main {
    background-color: var(--DarkDesaturatedBlue);
    color: var(--LightGrayishBlue);
    box-shadow: 5px 8px 20px 1px var(--DarkBlue);
    /* border: solid red; */
  }
  .todo-display-dark-tool-box {
    box-shadow: 5px 8px 20px 1px var(--DarkBlue);
  }
  .todo-display {
    display: flex;
    flex-direction: column;
    margin: 0 auto;
    width: 100%;
    border-radius: 10px;
    padding-right: 20px;
    padding-left: 20px;
    /* border: solid red; */
  }
  .mobile-view {
    display: flex;
    /* border: solid; */
    padding-left: 20px;
    padding-right: 20px;
    height: 55px;
  }
  .item-info-no-display {
    display: none;
  }
  .tool-box {
    /* border: solid red; */
    height: 55px;
    margin-top: 20px;
    border-top-left-radius: 6px;
    border-top-right-radius: 6px;
    padding-right: 40px;
    padding-left: 40px;
  }
  .all {
    margin-left: 0;
  }
  .btn,
  .item-info {
    font-size: 1.2rem;
  }
}
@media screen And (min-width: 768px) And (max-width: 821px) {
}
</style>
