<template>
    <div>
        <h1 v-text="name"></h1>
        <h3>Question number {{number }}/{{ Questions.length }}</h3>
         <h1>Score:{{points  }}</h1>
       <h3>{{ Questions[number-1].question }}</h3>
      
        <ul>
          
            <li v-for="(option) in Questions[number-1].options" :key='option'>
                <button  @click="selectAnswer(option,Questions[number-1].answer)">
                    {{option }}
                </button>
            </li>
        </ul>
<div class="btn">
    <button @click="previous">Previous</button>
    <button @click="next">Next</button>
</div>
    </div>
</template>
<script>
export default {
    data(){
        return{
            name:'Quiz App',
            number:1,
            points:0,

           
            Questions:[{
                question:'eeeee',
                options: ['asassss','bggghjjjj','big','small'],
                answer:'small',

            },
            {
                question:'jjjjkkk', 
                options:['home','back','come','jack'],
                answer:'home',

            },
            {
                question:'rrrrr',
                options:'',
                answer:'',

            }
        ]
        }

    },
    methods:{
        next(){
            if(this.QuestionsLength>this.number)
            this.number++
        },
        previous(){
            if(this.number>1){
                this.number--
                
            }
        },
        selectAnswer(option,answer){
            console.log(option)
            if(answer===option){
                console.log(answer)
                this.points++
            }
        },
    },
    computed:{
        QuestionsLength(){
            return this.Questions.length
        }
    }
  
    
}
</script>
<style scoped>

</style>