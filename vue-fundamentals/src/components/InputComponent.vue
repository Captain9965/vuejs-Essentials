<script>
import { store } from '../store/store';
export default{
    data(){
        return{
            store,
            input: "",
            
        }
    },
}
</script>
<template>
    <p>
      The message is {{ input }}
    </p>
    <textarea v-model="input" placeholder="Type your message here"/>
    <br>
    <br>
    <span> This is the store count: {{ store.count }}</span>
</template>
