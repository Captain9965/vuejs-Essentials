<!-- BlogPost.vue -->
<script>
export default {
  props: ['title','key']
}
</script>

<template>
  <h4> {{key}} {{ title }}</h4>
</template>