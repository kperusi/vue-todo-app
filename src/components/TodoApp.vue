<template>
  <div>
    <h1>Todo App</h1>
    <div>
      <ul class="item-container">
        <li v-for="(todo, i) in todos" :key="i">{{ i + 1 }}
          <input  @click="onEdit(todo)" readonly='true' :value ='todo.name' :class="{'has-line-through': todo.isCompleted}"/>
            <!-- <span :class="{'has-line-through': todo.isCompleted}">{{ i + 1 }} {{ todo.name }}</span> -->
            <button @click="onComplete(todo)">{{todo.isCompleted?'Undo':'Completed'}}</button>
            <button @click="onRemove(todo.id)">Delete</button>
        </li>
      </ul>
    </div>
    <div class="input-container">
      <label for="todoinput">Enter a todo item</label>
      <input type="text" name="todoinput" v-model="todo" />
      <button @click="AddTodos"  :disabled="!todo">Add Todo Item</button>
    </div>

  </div>
</template>

<script>
export default {
  name: "TodoApp",
  data() {
    return {
      todo: "",
      todos: [
        {
          id: 1,
          name: "Buy Ice",
          isCompleted: false,
        },
      ],
    };
  },
  methods: {
    AddTodos() {
      this.todos.push({
        name: this.todo,
        id: this.todos.length + 1,
        isCompleted: false,
      }),
        (this.todo = "");
    },
    onChangeHandler(event) {
      this.todo = event.target.value;
    },
    onComplete(item) {
     item.isCompleted=!item.isCompleted
    },

    onRemove(id){
        this.todos = this.todos?.filter((todo) => todo.id !== id);
  
    },
    onEdit(todo){
      console.log(todo.id)
      console.log(todo.name)


    }


  },
};
</script>

<style>
.input-container {
  display: flex;
  flex-direction: column;
  width: 200px;
  margin: 0 auto;
}

.item-container {
  
  list-style: none;
  font-weight: 700;
  text-align: justify;
  width: 400px;
  margin: 30px auto;
  border: 1.5px solid rgb(201, 200, 200);
  gap: 10px;
}
.item-container li{
    display: flex;
    gap: 20px;
margin:10px;
}
.has-line-through{
    background: rgb(54, 219, 244);
    text-decoration: line-through;
    color:white
}
</style>