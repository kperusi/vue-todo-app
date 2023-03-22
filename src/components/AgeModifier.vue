<template>
    <div>
      <input type="number" v-model="inputValue" />
      <button @click="$emit('add-age', inputValue)">Add age</button>
      <button @click="$emit('multiply-age', inputValue)">Multiply age</button>
    </div>
  </template>
  

  <script>
  export default {
    name: "AgeComponent",
    data() {
      return {
        inputValue: 5,
      };
    },
  };
  </script>