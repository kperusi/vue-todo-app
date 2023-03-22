<script>
import link from "./images/icon-sun.svg";
export default {
  props: ["Theme", "toogleThemes"],
  data() {
    return {
      link: link,
    };
  },

  emits: ["theme"],
  methods: {},
};
</script>

<template>
  <div class="nav">
    <h1>TODO</h1>
    <span
      class="imgs"
      @click="$emit('theme')"
      :class="toogleThemes ? Theme.darkTheme.moon : Theme.lightTheme.sun"
    ></span>
  </div>

  <!-- <div>{{ Theme }}</div> -->
</template>

<style scoped>
.nav {
  /* border: 1px solid grey; */
  display: flex;
  margin: 0px auto;
  width: 40%;
  
  color: white;
}
.imgs {
  height: 30px;
  margin-left: auto;
  /* border: solid; */
  width: 30px;
  margin-top: auto;
  margin-bottom: auto;
  background-image: url(./images/icon-moon.svg);
  background-repeat: no-repeat;
}
.imgs:hover {
  cursor: pointer;
}
.moon{
  background-image: url(./images/icon-sun.svg);
}
.sun{
    
    background-image: url(./images/icon-moon.svg); 
}

@media screen And (min-width:180px) And (max-width:767px) {
  .nav {
  /* border: 1px solid grey; */
  display: flex;
  margin: 0px auto;
  width: 100%;
  color: white;
  padding-left: 20px;
  padding-right: 20px;
}

  
}
@media screen And (min-width:768px) And (max-width:821px) {
  
}
</style>
