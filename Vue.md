# Vue Introduction:

This is a javascript, HTML and CSS-based framework that provides a declarative, component-based programming model. 

2 core features of vue:

1. **declarative rendering** - Vue extends standard HTML that allows one to declaratively describe HTML output based on a Javascript state.
2. **Reactivity** - vue automatically tracks js state changes and efficiently updates the DOM when changes happen.

## The Progessive framework:

Vue can be used in different ways:<br>
1. Enhancing static HTML without a build step
2. Embedding as web components on any page
3. Single-page applications
4. Full-stack/server-side-rendering
5. Jam-stack/server-side-generation
6. Targeting desktop, mobile, WebGL and even the terminal.

vue is very convenient for users, both newbies and experts as it can be easily tweaked to solve may problems.

## Single File Components:

Vue is formatted using a HTML-like file format called **singe-file-Component** which encapsulates the component's logic(js), its template(HTML) and styles(CSS) in a single file.

## API styles:
### Options API:

Here, we define a component's logic using an object of options such as data, methods and mounted. Properties defined by options are exposed on this inside functions, which points to the component instance.
Interestingly, this is implemented on top of the composition API
It is centerd around component instance, hence the use of `this`. It lends itself to users with an OOP background, more beginner friendly and more organized by enforcing code organization via option groups.

```
<script>
export default {
  // Properties returned from data() become reactive state
  // and will be exposed on `this`.
  data() {
    return {
      count: 0
    }
  },

  // Methods are functions that mutate state and trigger updates.
  // They can be bound as event listeners in templates.
  methods: {
    increment() {
      this.count++
    }
  },

  // Lifecycle hooks are called at different stages
  // of a component's lifecycle.
  // This function will be called when the component is mounted.
  mounted() {
    console.log(`The initial count is ${this.count}.`)
  }
}
</script>

<template>
  <button @click="increment">Count is: {{ count }}</button>
</template>
```

### Composition API:

Here, we define a component's logic using imported API functions. In SFC's, it is typically used with `<script setup>` the `setup` is a hint to make vue make compile-time transforms that allow us to use Composition APIs with less boilerplate. For example, imports and top level variables and functions are directly usable in the template.

It is centerd around declaring reactive state variables directly in a function scope and composing state from multiple functions together to handle complexity. 

It is consequently more flexible and enables more powerful patterns for organizing and reusing logic.

```
<script setup>
import { ref, onMounted } from 'vue'

// reactive state
const count = ref(0)

// functions that mutate state and trigger updates
function increment() {
  count.value++
}

// lifecycle hooks
onMounted(() => {
  console.log(`The initial count is ${count.value}.`)
})
</script>

<template>
  <button @click="increment">Count is: {{ count }}</button>
</template>
```
### Quick Start:

Vue's build system is based on **vite** which is a common frontend build tool
Before beginning, ensure you have node.js installed.

To install vue, type in the following command:<br>
`npm init vue@latest`
