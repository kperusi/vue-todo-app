<template>
    <div id="app">
      <div>
        <label for="age">Age:</label>
        <input id="age" type="number" v-model="age" />
      </div>
      <div id="np-age-modifier-component">
        <AgeModifierComponent @add-age="addToAge" @multiply-age="multiplyByAge" />
      </div>
    
    </div>
  </template>
  
  <script>

  import AgeModifierComponent from "./AgeModifier";
  
  export default {
    name: "App",
    components: { AgeModifierComponent },
    data() {
      return {
        age: 27,
      };
    },
    methods: {
      addToAge(newAge) {
        this.age = parseInt(this.age, 10) + parseInt(newAge, 10);
      },
      multiplyByAge(newAge) {
        this.age = parseInt(this.age, 10) * parseInt(newAge, 10);
      },
    },
  };
  </script>
  
  <style>
  #app {
    font-family: "Avenir", Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    padding: 20px;
    background: rgb(247, 247, 247);
    border: 1px solid rgb(223, 223, 223);
    border-radius: 4px;
    max-width: 400px;
  }
  #np-age-modifier-component {
    margin-top: 24px;
  }
  button {
    background: rgb(40, 59, 230);
    color: #fff;
    border: 0px;
    padding: 6px 8px;
    margin-left: 10px;
    border-radius: 4px;
  }
  input {
    background: rgb(226, 226, 226);
    color: rgb(26, 26, 26);
    border: 0px;
    padding: 6px 8px;
    margin-left: 6px;
    outline: none;
    border-radius: 4px;
  }
  #np-credits {
    margin-top: 12px;
    color: rgb(170, 170, 170);
  }
  </style>
  