<script>
import { computed } from '@vue/reactivity'
import  InputComponent  from './components/InputComponent.vue'
import blogPost from './components/blogPost.vue'
import BlogPost from './components/blogPost.vue'
import {store} from './store/store'
  export default{
    data() {
        return {
            store,
            list: ["lenny", "James", "Cephas"],
            msg: "Hello World",
            rawHTML: "<span style=\"color: red\">This should be red.</span>",
            posts: [
              { id: 1, title: 'My journey with Vue' },
              { id: 2, title: 'Blogging with Vue' },
              { id: 3, title: 'Why Vue is so fun' }]
        };
    },
    components:{
      InputComponent,
      blogPost
    },
    methods: {
        changeMsg() {
            store.increment();
            this.msg = "Happy coding";
        },
        returnMsg() {
            store.increment();
            this.msg = "Hello World";
        },
        greet(event) {
            //this inside methods indicate the current active instance:
            alert(`Hello ${this.name}`);
            if (event) {
                alert(event.target.tagName);
            }
        }
    },
    mounted() {
        console.log(this.$refs.items);
        this.returnMsg();
    },
    computed: {
        countExceeded() {
            return store.count > 5 ? "Count is greater than 5" : "Count is less than 5";
        }
    },
    components: { InputComponent, BlogPost }
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
   <InputComponent/>
   <BlogPost 
      v-for = "post in posts"
      :key ="post.id"
      :title = "post.title"
      />
  </main>
</template>

<style scoped>
</style>
