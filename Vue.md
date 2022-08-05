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
`npm init vue@latest`<br>
This command will execute **create-vue** which is the official vue project scaffolding tool. 

In you project folder,execute the following to install dependencies and to start the dev server:<br>
`npm install` <br>
`npm run dev`

### The application instance:

Every vue application begins by creating an application instance with the `createApp` function.

```
import { createApp } from 'vue'

const app = createApp({
  /* root component options */
})

```

### The Root App component:

This is the object that is passed as an argument to the createApp function which is a component containing other components as its children.

In SFC, we typically import this component from another file:

```
import { createApp } from 'vue'
// import the root component App from a single-file component.
import App from './App.vue'

const app = createApp(App)

```

### Mounting the App:

An application instance will not render anything unless its `mount()` method is called. It expects a container argument which can be an actual DOM element or a selector string.

`<div id="app"></div>`<br>
`app.mount('#app')`<br>
The content of the app's root component will be rendered insinde the container element. The container element is not considered part of the app.
The mount method should only be called after all configurations and and asset registrations are done. Its return value is the root component instance and not the application instance.


### App Configurations:

The application instance provides a .config() object that allows one to configure a few app-level options like defining an error handler that captures errors from all descendent components.
```
app.config.errorHandler = (err) => {
  /* handle error */
}

```
One can also register app-scoped assets like:
```
app.component('TodoDeleteButton', TodoDeleteButton)

```
This allows **TodoDeleteButton** to be used anywhere in our application.

Remember that all configurations need to be applied before mounting the app!!


### Multiple application instances:

The **createApp** API allows multiple vue applications to co-exist in the same page.
```
const app1 = createApp({
  /* ... */
})
app1.mount('#container-1')

const app2 = createApp({
  /* ... */
})
app2.mount('#container-2')
```

## Template Syntax:

Vue uses a HTML-based Syntax that allows one to declaratively bind the rendered DOM to the underlying components instance data. All vue templates are syntactically valid HTML that can be parsed by HTML compliant parsers
Under the hood, vue compiles the template code into highly-optimized js code and combined with the reactivity system, vue is able to intelligently figure out the minimum components to rerender and apply the minimal amount of DOM manipulations when the app state changes.

### Text Inerpolation:

This uses the Moustache syntax(double curly braces):
`<span>Message: {{ msg }}</span>`

The Moustache tag will be replaced with the value of the `msg` property from the corresponding component instance. Will also be updated when it changes. 