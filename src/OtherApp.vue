<template>
<div>
    <div>this is another {{names}}</div>
    <h1>{{msgs}} to {{names}}</h1>

    <h2 v-if="users.firstName">Welcome, {{users.firstName}}</h2>
    <h1 v-else-if="users.lastName"> Welcome {{users.lastName}}</h1>
    <div v-else>
        <button>Register</button>
        <button>Login</button>
    </div>

    <div v-show="isLoggedIn">
        <p>you are logged in</p>
    </div>
    <div v-show="!isLoggedIn">
        <p>you are not logged in</p>
    </div>

    <button v-on:click.once='clickme()'>Touch Me</button>
     <button :class="red" @click='clickme2()'>Touch Me</button>
    
</div>
    


</template>
<script>
export default {
    name:'otherApp', 
    data(){
        return{
             names:'otherApp',
             todos:[],
             users:{
                firstName:'sam',
                lastName:'black',
                username:'samBlack'
             },
             isLoggedIn:false,
             red:""
        }
       
    },
    props:{
        msgs:String
    },

    methods:{
        clickme(){
            alert('you clicked me')
        },
        clickme2(){
            if(this.red==='red'){
                this.red =""
            }
            else{
                this.red = 'red'
            }
          
        }
    }
   
}
</script>
<style>
.red{
    background: red;
}
</style>