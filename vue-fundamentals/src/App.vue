<script>
import { computed } from '@vue/reactivity'

  export default{
    data(){
      return{
        count : 0,
        list : ["lenny", "James", "Cephas"],
        msg: "Hello World",
        input:"nothing",
        rawHTML: '<span style="color: red">This should be red.</span>'
      }
    },
    methods:{
      changeMsg(){
        this.count++
        this.msg = "Happy coding"
      },
      returnMsg(){
        this.count++
        this.msg = "Hello World"
      },
      greet(event){
        //this inside methods indicate the current active instance:
        alert(`Hello ${this.name}`)
        if (event){
          alert(event.target.tagName)
        }

      }
    },
    mounted(){
      console.log(this.$refs.items)
      this.returnMsg()
    },
    computed: {
      countExceeded(){
        return this.count > 5 ? 'Count is greater than 5': 'Count is less than 5'
      }

    }
  }
</script>

<template>
  <header>
  </header>
  <main>
    <p>
      {{ msg }}
    </p>
    <button @click="changeMsg"> Change Message</button>
    <br>
    <br>
    <button @click="returnMsg"> Return Message</button>
    <br>
    <br>
    <p>Using v-html directive: <span v-html="rawHTML"></span></p>
    <p>
      <span>{{ countExceeded }}</span>
    </p>
    <li v-for="(list_items,index) in list" ref="items">
    {{ index}} - {{ list_items }} 
    </li>
     <br>
    <br>
    <button @click="greet"> Greet me! </button>
    <p>
      The message is {{ input }}
    </p>
    <textarea v-model="input" placeholder="Type your message here"/>
  </main>
</template>

<style scoped>
</style>
