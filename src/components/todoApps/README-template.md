# Frontend Mentor - Todo app solution

This is a solution to the [Todo app challenge on Frontend Mentor](https://www.frontendmentor.io/challenges/todo-app-Su1_KokOW). Frontend Mentor challenges help you improve your coding skills by building realistic projects. 

## Table of contents

- [Overview](#overview)
  - [The challenge](#the-challenge)
  - [Screenshot](#screenshot)
  - [Links](#links)
- [My process](#my-process)
  - [Built with](#built-with)
  - [What I learned](#what-i-learned)
  - [Continued development](#continued-development)
  - [Useful resources](#useful-resources)
- [Author](#author)
- [Acknowledgments](#acknowledgments)

**Note: Delete this note and update the table of contents based on what sections you keep.**

## Overview
This is a solution to Todo app challenge on Frontend Mentor on. I have built this app using  the popular javascript frame work vue js. With this app users can Enter their day to day TODOs, Mark their completed TODOs,view all their ACTIVE TODOs, View their completed TODOS, delete their any item on their TODO,deleted or clear their completed TODOS and event drag and drop any TODO item to re order the TODO order. Users can also select their prefered Themes. this app is also built with localstorage to make sure states ared stored on browsers memory.
I have used SASS and css module for my styling. 

### The challenge

Users should be able to:
- View the optimal layout for the app depending on their device's screen size
- See hover states for all interactive elements on the page
- Add new todos to the list
- Mark todos as complete
- Delete todos from the list
- Filter by all/active/complete todos
- Clear all completed todos
- Toggle light and dark mode
- **Bonus**: Drag and drop to reorder items on the list

### Screenshot

![](./src/assets/myvue-app.png)

### Links

- Solution URL: (https://github.com/kperusi/vue-todo-app)
- Live Site URL:(https://vue-todo-app-fame.vercel.app/)

## My process

### Built with

- Vue Js
- CSS and SASS 
- Flexbox
- Mobile-first workflow
- [Vue ](https://vuejs.org/) - JS Framework



### What I learned
I also learnt working with javascript filter
Javascript localstorage

To see how you can add code snippets, see below:

```js
cconst removeCompleted = () => {
  alltodos.value = alltodos.value.filter(function (each) {
    return each.completed !== true;
  });
  todos.value = alltodos.value;
};

onMounted(() => {


  if (localStorage.alltodos!='') {
    
    alltodos.value = JSON.parse(localStorage.getItem("alltodos")) || [];
    todos.value = alltodos.value;
   
  } else {

    localStorage.setItem("alltodos", JSON.stringify(alltodos.value));
    console.log(JSON.parse(localStorage.getItem('alltodos')))
  }
  
});

```

### Continued development
I will like to work more with vue js and using vuex to manage my state.
I will also want to work on using more than only two themes.

### Useful resources

- [Example resource 1](https://vuejs.org/) - This helped me with the documentation of vue js.
- [Example resource 2](https://javascript.info/) - I used this resources to learn more about local storage



## Author

- Website - [Sunday Famous](https://superlative-gaufre-08fa5e.netlify.app/)
- Frontend Mentor - [@kperusi](https://www.frontendmentor.io/profile/kperusi)
- Twitter - [@sundayfamous5](https://twitter.com/FamousSunday5)

## Acknowledgments
Frontend mentors
