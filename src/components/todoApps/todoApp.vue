<script setup>
import NavBar from "./NavBar.vue";
import todoDisplay from "./todoDisplay.vue";
import { ref } from "vue";
import { onMounted, watch } from "vue";

const toogleThemes = ref("");

let Theme = ref({
  darkTheme: {
    moon: "moon",
    todomainStyles: "todo-mains",
    todoDisplaydarkMain: "todo-display-dark-main",
    todoDisplayDarkToolBox: "todo-display-dark-tool-box",
    inputDark: "input-dark",
    activeDark: "active-dark",
    completedDark:'completed-dark'
  },
  lightTheme: {
    sun: "sun",
    todomainStyles: "light-todo-mains",
    todoDisplayLightMain: "todo-display-light-main",
    todoDisplayLightToolBox: "todo-display-light-tool-box",
    inputLight: "input-light",
    activeLight: "active-light",
    completedLight:'completed-light'
  },
});

const themeToggle = () => {
  if (toogleThemes.value === true) {
    toogleThemes.value = false;
  } else toogleThemes.value = true;
};

watch(toogleThemes, (newVal) => {
  localStorage.setItem("toogleThemes", newVal);
});

onMounted(() => {
  toogleThemes.value = JSON.parse(localStorage.getItem("toogleThemes"));
});
</script>

<template>
  <div
    class="todo-main"
    :class="
      toogleThemes
        ? Theme.darkTheme.todomainStyles
        : Theme.lightTheme.todomainStyles
    "
  >
    <NavBar @theme="themeToggle" :Theme="Theme" :toogleThemes="toogleThemes" />
    <todoDisplay :Theme="Theme" :toogleThemes="toogleThemes" />
    <p class="drag">Drag and drop to re-order list</p>
  </div>
</template>
<style>
:root {
  --VeryLightGray: hsl(0, 0%, 98%);
  --VeryLightGray: hsl(0, 0%, 98%);
  --VeryLightGrayishBlue: hsl(236, 33%, 92%);
  --LightGrayishBlue: hsl(233, 11%, 84%);
  --DarkGrayishBlue: hsl(236, 9%, 61%);
  --VeryDarkGrayishBlue: hsl(235, 19%, 35%);

  --DarkBlue: hsl(235, 21%, 11%);
  --DarkDesaturatedBlue: hsl(235, 24%, 19%);
  --LightGrayishBlue: hsl(234, 39%, 85%);
  --LightGrayishBluehover: hsl(236, 33%, 92%);
  --DarkGrayishBlue: hsl(234, 11%, 52%);
  ----VeryDarkGrayishBlue: hsl(233, 14%, 35%);
  --VeryDarkGrayishBlue2: hsl(237, 14%, 26%);
}
* {
  box-sizing: border-box;
}
@font-face {
  font-family: "Josefin_Sans";
  src: url("@/assets/Josefin_Sans/static/JosefinSans-Regular.ttf");
}

body,
html,body {
  padding: 0;
  margin: 0;
  font-family: "Josefin_Sans";
  font-weight: 100;
  
}

.todo-main {
  display: flex;
  flex-direction: column;
  background-repeat: no-repeat;
  background-position: top;
  background-size: 100% 300px;
  padding-bottom: 3px;
 
 
}
.drag {
  /* border: solid; */
  height: 60px;
  text-align: center;
  padding-top: 20px;
  color: var(--VeryDarkGrayishBlue);
}

.todo-mains {
  background-image: url(./images/bg-desktop-dark.jpg);
  background-color: hsl(235, 21%, 11%);
}
.light-todo-mains {
  background-image: url(./images/bg-desktop-light.jpg);
  background-color: var(--VeryLightGray);
}
@media screen And (min-width: 180px) And (max-width: 767px) {
  .todo-main {
    background-size: 100% 200px;
    padding-bottom: 3px;
   
  }

  .todo-mains {
    background-image: url(./images/bg-mobile-dark.jpg);
    background-color: hsl(235, 21%, 11%);

  }
  .light-todo-mains {
    background-image: url(./images/bg-mobile-light.jpg);
    background-color: var(--VeryLightGray);
    /* border: solid red; */
  }
}
@media screen And (min-width: 768px) And (max-width: 821px) {
  .todo-mains {
    background-image: url(./images/bg-mobile-dark.jpg);
    background-color: hsl(235, 21%, 11%);
  }
  .light-todo-mains {
    background-image: url(./images/bg-mobile-light.jpg);
    background-color: var(--VeryLightGray);
  }
}
</style>
