<script>
  export default{
    data(){
      return{
        count : 0,
        msg: "Hello World"
      }
    },
    methods:{
      changeMsg(){
        this.msg = "Happy coding"
      },
      returnMsg(){
        this.msg = "Hello World"
      }
    },
    mounted(){
      this.returnMsg()
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
  </main>
</template>

<style scoped>
</style>
