<script>
import { computed } from '@vue/reactivity'

  export default{
    data(){
      return{
        count : 0,
        msg: "Hello World",
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
      }
    },
    mounted(){
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
  </main>
</template>

<style scoped>
</style>
