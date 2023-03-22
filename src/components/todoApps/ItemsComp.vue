<script>
export default {
  props: ["todos"],
  data() {
    return {};
  },
  emits: ["removeTodo"],
  methods: {
    setCompleted(todo) {
      if (todo.completed === true) {
        todo.completed = false;
      } else {
        todo.completed = true;
      }
    },
    setMouseEnter(todo) {
      todo.onMouseEnter = true;
    },

    setMouseLeave(todo) {
      todo.onMouseEnter = false;
    },

    startDrag(e) {
      const target = e.target;
      e.dataTransfer.dropEffect = "move";
      e.dataTransfer.effectAllowed = "move";
      e.dataTransfer.setData("itemId", target.id);
      console.log(target.id);
     
    },
  },
};
</script>

<template>
  <div class="item">
    <div
      class="todo-wrap"
      v-for="todo in todos"
      :key="todo.id"
      draggable="true"
      :id="todo.id"
      @dragstart="startDrag"
      @dragover.stop

     @mouseenter="setMouseEnter(todo)"
     @mouseleave="setMouseLeave(todo)"
    >
      <span class="check-wrap-brd"
        :class="{ 'check-wrap': 'check-wrap', completed: todo.completed }"
        @click="setCompleted(todo)"
      ></span>
      <p class="todo-name" :class="{ 'line-through': todo.completed }">
        {{ todo.name }}  </p>
      <div
        v-show="todo.onMouseEnter"
        class="cross"
        @click="$emit('removeTodo', todo.id)"
      >
        <img src="./images/icon-cross.svg" alt="cross" style="width: 14px" />
      </div>
    </div>
  </div>
</template>

<style scoped>
.item {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 10px;
 
 
}

.todo-wrap {
  display: flex;
  flex-direction: row;
  align-items: center;
  border-bottom: 1px solid grey;
  width: 100%;
  
  padding-bottom: 5px;
 

}
.check-wrap {
  border-radius: 50%;
  width: 30px;
  height: 30px;
  border: 0.1px solid rgba(128, 128, 128, 0.353);
  margin-left: 20px;
}
.check-wrap:hover {
  cursor: pointer;
  border: 0.1px solid rgb(128, 128, 128);
}
.todo-name {
  margin-left: 15px;
}
.img-wrap:hover {
  cursor: pointer;
}
.cross {
  margin-left: auto;
  margin-right: 20px;
  width: 15px;
  height: 15px;
}
.item:hover {
  cursor: pointer;
}
.cross:hover {
  cursor: pointer;
}
.completed {
  background-image: url(./images/icon-check.svg),
    linear-gradient(hsl(192, 100%, 67%), hsl(280, 87%, 65%));
  background-repeat: no-repeat;
  background-size: 20px, cover;
  background-position: center;
}
.line-through {
  text-decoration: line-through;
  color: rgba(128, 128, 128, 0.393);
}

.block {
  display: block;
}

/* _________________//mobile 1 ________________*/

@media screen And (min-width: 180px) And (max-width: 767px) {
  .item {
    display: flex;
    flex-direction: column;
    align-items: center;
    width: 100%;
  

  }

  .todo-wrap {
    display: flex;
    flex-direction: row;
    align-items: center;
    border-bottom: 1px solid grey;
    width: 100%;
    font-size: 1.2rem;
  }
}
@media screen And (min-width: 768px) And (max-width: 821px) {
}
</style>
