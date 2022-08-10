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

###  Raw HTML:

{{ }} outputs data as text. the `v-html` directive has to be used to ouptput raw html.

```
<p>Using text interpolation: {{ rawHtml }}</p>
<p>Using v-html directive: <span v-html="rawHtml"></span></p>

```
`v-` indicates that this is a special directive provided by vue.
Note that one cannot use `v-` to compose template partials because vue is not a string based templating engine. Furthermore, components are preferred as the fundamental unit for UI reuse and composition. `v-html` should never be used on user-provided content as this may lead to vulnerability to XSS attacks.


### Attribute Bindings

Moustaches cannot be used inside HTML attributes. Instead, a `v-bind` directive should be used.ie: 
```
<div v-bind:id="dynamicId"></div>
or
<div :id="dynamicId"></div>

```
This, for example, instructs vue to keep the `id` attribute of the element in sync with the component's `dynamicId` property.If the bound value is `null` or `undefined`, then it is removed from the rendered element. The shorthand for this is `:id` and is the most commonly used syntax among developers.


### Boolean Attributes:

Are attributes that indicate true or false by its prescence on an element. `v-bind` works a little different in this case:
```
<button :disabled="isButtonDisabled">Button</button>

```
So the disabled attribute will be included if disabled has a truthly value and not included if it has a falsely value. Note that "" is a truthly value.

### Dynamically binding multiple attributes:

```
data() {
  return {
    objectOfAttrs: {
      id: 'container',
      class: 'wrapper'
    }
  }
}
```

And can be bound to a single element using `v-bind` without an argument:

```
<div v-bind="objectOfAttrs"></div>

```
### Using JS Expressions:


```
{{ number + 1 }}

{{ ok ? 'YES' : 'NO' }}

{{ message.split('').reverse().join('') }}

<div :id="`list-${id}`"></div>

```
These expressions will be evaluated in the data scope of the current component instance. As above, js expressions can only be used in the following positions:

1. Inside Moustaches
2. Inside attribute values of any vue directives

### Expressions only:

Each binding can only contain one singe expression. An expression must evaluate to a value. 

### Calling Functions:

It is possible to call a component-exposed method inside a binding expression:

```
<span :title="toTitleDate(date)">
  {{ formatDate(date) }}
</span>

```
However, since functions called inside binding expressions will be called every time the component updates, they should not have any side-effects such as changing data or triggerint asynchronous operations.

### Restricted Global Access:

Template expressions are sandboxed and only have access to a restricted list of globals..like Math and Date..One can however add others to `app.config.globalProperties`

### Directives:

These are special attributes with the `v-` prefix. Attribute values are expected to be singe js expressions with the exception of `v-for, v-on, v-slot`.

A directive's job is to apply changes to the DOM when the value of its expression changes. 

eg.
```
<p v-if="seen">Now you see me</p>
```
is supposed to insert/remove the `<p>` element based on the truthliness of the value of the expression `seen`

### Arguments:

Some directives can take arguments such as the `v-bind` directive, which is denoted by a colon after the directive name. 
And example is the `v-on` directive which listens to DOM events:

```
<a v-on:click="doSomething"> ... </a>

<!-- shorthand -->
<a @click="doSomething"> ... </a>

```
### Dynamic arguments:



It is possible to use js expressions in a directive argument by wrapping it inside square brackets.

```
<!--
Note that there are some constraints to the argument expression,
as explained in the "Dynamic Argument Value Constraints" and "Dynamic Argument Syntax Constraints" sections below.
-->
<a v-bind:[attributeName]="url"> ... </a>

<!-- shorthand -->
<a :[attributeName]="url"> ... </a>

<a v-on:[eventName]="doSomething"> ... </a>

<!-- shorthand -->
<a @[eventName]="doSomething">
```
### Dynamic argument Value Constraints:

Dynamic arguments are expected to evaluate to a string except `null` which is used to explicitly remove the binding. Any other non-string value will trigget a warning. 

### Dynamic arguments Syntax constraints:

This is necessary because HTML attribute names do not have charactes like spaces or quotes. 
When using in-DOM templates, one should avoid using upper-case letters as attribute names because html coerces them to lower-case letters.
Templates inside SFC components are not affected.

### Modifiers:

Indicate that a directive should be bound in a special way.
For example, the `.prevent` modifier in this case tells `v-on` directive to call `event.preventDefault()` on the triggered event.

```
<form @submit.prevent="onSubmit">...</form>

```
## Reactivity Fundamentals:

### Declaring a reactive state:

In Options API, we use the `data()` option to declare the reactive state of a component. The option value should be an object that returns an object. Vue will call the function when creating a new component instance and wrap the returned object in its reactivity system. Any top-level properties of this object are proxied on the component instance. (`this` in methods and lifecycle hooks.)

```
export default {
  data() {
    return {
      count: 1
    }
  },

  // `mounted` is a lifecycle hook which we will explain later
  mounted() {
    // `this` refers to the component instance.
    console.log(this.count) // => 1

    // data can be mutated as well
    this.count = 2
  }
}
```
These instance objects are only added when the instance is first created. Hence, ensure that they are all present in the object returned in the `data` function. use `null` or `undefined` if they are not yet available. 

It is possible to add properties directly to `this` without including it in data. However, they cannot trigger reactive updates.
Vue uses a `$` prefix when exposing its own built-in APIs via the component instance and _ for internal properties.

### Reactive Proxy vs Original:

```
export default {
  data() {
    return {
      someObject: {}
    }
  },
  mounted() {
    const newObject = {}
    this.someObject = newObject

    console.log(newObject === this.someObject) // false
  }
}
```
When accessing the value of `this.someObject`, the value is a reactive proxy of the original `newObject`. The original `newObject` is left intact and is not made reactive. One must make sure to always access reacitve state as a property of `this`

## Declaring methods:

The `methods` option is used to add methods to a component instance..ie
```
export default {
  data() {
    return {
      count: 0
    }
  },
  methods: {
    increment() {
      this.count++
    }
  },
  mounted() {
    // methods can be called in lifecycle hooks, or other methods!
    this.increment()
  }
}
```
Vue automatically binds the `this` value for methods so that it always refers to the component instance. This ensures that it always maintains the correct value of `this` if it is used as an event callback or listener. Avoid using arrow functions when defining methods as this prevents vue from binding the appropriate `this` value. ie.
 ```
  increment: () => {
      //no access to this here!
    }
```
Like the properties of the component instance, the methods are accessible within the components template..usually as event listeners..
```
<button @click="increment">{{ count }}</button>
```
## DOM Update Timing:

When one mutates a reactive state, the DOM mutates automatically, by buffering them until the next 'tick' in the upddate cycle to ensure each component updates only once no matter how many state changes one makes.
One can use the `nextTick()` global API to wait for the DOM update to complete after a state change.
```
import { nextTick } from 'vue'

export default {
  methods: {
    increment() {
      this.count++
      nextTick(() => {
        // access updated DOM
      })
    }
  }
}
```
## Deep Reactivity:

Vue can detect changes even in nested objects or arrays:
```
export default {
  data() {
    return {
      obj: {
        nested: { count: 0 },
        arr: ['foo', 'bar']
      }
    }
  },
  methods: {
    mutateDeeply() {
      // these will work as expected.
      this.obj.nested.count++
      this.obj.arr.push('baz')
    }
  }
}
```
## Stateful Methods:
In some cases, it is necessary dynamically create a method function, for instance a debounced event handler:
```
import { debounce } from 'lodash-es'

export default {
  methods: {
    // Debouncing with Lodash
    click: debounce(function () {
      // ... respond to click ...
    }, 500)
  }
}
```
However, if multiple component instances share the same debounced function, they will interfere with one another since a debounced function is stateful: it maintains its own internal state.
A way to solve this is to create the debounced version in the `created` lifecycle hook:
```
export default {
  created() {
    // each instance now has its own copy of debounced handler
    this.debouncedClick = _.debounce(this.click, 500)
  },
  unmounted() {
    // also a good idea to cancel the timer
    // when the component is removed
    this.debouncedClick.cancel()
  },
  methods: {
    click() {
      // ... respond to click ...
    }
  }
}
```

## Computed Properties:

In template expressions are only meant for simple operations. It can quickly get cluttered as shown:
```
export default {
  data() {
    return {
      author: {
        name: 'John Doe',
        books: [
          'Vue 2 - Advanced Guide',
          'Vue 3 - Basic Guide',
          'Vue 4 - The Mystery'
        ]
      }
    }
  }
}
``` 
and 
```
<p>Has published books:</p>
<span>{{ author.books.length > 0 ? 'Yes' : 'No' }}</span>
```
This is where a computed property comes in:

```
export default {
  data() {
    return {
      author: {
        name: 'John Doe',
        books: [
          'Vue 2 - Advanced Guide',
          'Vue 3 - Basic Guide',
          'Vue 4 - The Mystery'
        ]
      }
    }
  },
  computed: {
    // a computed getter
    publishedBooksMessage() {
      // `this` points to the component instance
      return this.author.books.length > 0 ? 'Yes' : 'No'
    }
  }
}
```
and:
```
<p>Has published books:</p>
<span>{{ publishedBooksMessage }}</span>
```

### Computed Caching vs Methods:

We can achieve the same result with:
```
// in component
methods: {
  calculateBooksMessage() {
    return this.author.books.length > 0 ? 'Yes' : 'No'
  }
}
```
and:
```
<p>{{ calculateBooksMessage() }}</p>
```

The end result is exactly the same. However, computed properties are cached based on their respective dependencies meaning that it will only be re-evaluated when any of its reactive dependencies have changed. Multiple function calls will only return the cached result.

As a result, the following will not run, since Date is not a reactive property:
```
computed: {
  now() {
    return Date.now()
  }
}
```
Method invocation will always work in this case.

### Writable Computed:

Computed properties are by default getter only. Vue raises a runtime error when one tries to assign a new value to a computed property. One can however do this through getters and setters.
```
export default {
  data() {
    return {
      firstName: 'John',
      lastName: 'Doe'
    }
  },
  computed: {
    fullName: {
      // getter
      get() {
        return this.firstName + ' ' + this.lastName
      },
      // setter
      set(newValue) {
        // Note: we are using destructuring assignment syntax here.
        [this.firstName, this.lastName] = newValue.split(' ')
      }
    }
  }
}
```
Now `this.fullName = 'John Doe'` will cause the setter to be invoked and `this.firstName` and `this.lastName` will be updated accordingly

Getters should be side effect-free which means that they should be purely computational functions that do not manipulate the DOM or make async requests.
]
## Class and style Bindings:
Since `class` and `style` are both attributes, they can be dynamically assigned to a string value with `v-bind`.

We can pass an object to `:class` to dynamically toggle classes. 
```
<div :class="{ active: isActive }"></div>

```
This means that the prescence of the `active` class is determined by the truthliness of the data property `isActive`.
The `:class` directive can co-exist with the plain `class` attribute.
```
data() {
  return {
    isActive: true,
    hasError: false
  }
}

<div
  class="static"
  :class="{ active: isActive, 'text-danger': hasError }"
></div>

```
will render:

```
<div class="static active"></div>
```

The class list will be updated accordingly. One can also do:
```
data() {
  return {
    classObject: {
      active: true,
      'text-danger': false
    }
  }
}
``` 
and:
```
<div :class="classObject"></div>
```
We can also bind to a computed property:

```
data() {
  return {
    isActive: true,
    error: null
  }
},
computed: {
  classObject() {
    return {
      active: this.isActive && !this.error,
      'text-danger': this.error && this.error.type === 'fatal'
    }
  }
}
```
and:
```
<div :class="classObject"></div>
```

### Binding to Arrays:
```
data() {
  return {
    activeClass: 'active',
    errorClass: 'text-danger'
  }
}
```
and:
```
<div :class="[activeClass, errorClass]"></div>
```
which will render:
```
<div class="active text-danger"></div>
```
We can also toggle the class in the list conditionally:
```
<div :class="[isActive ? activeClass : '', errorClass]"></div>
```
or since the above can become a bit verbose:
```
<div :class="[{ active: isActive }, errorClass]"></div>
```
## With components:

When one uses the `class` attibute on a component with a single root element, those components will be added to the components root element and merged with any existing class already on it. 
```
<!-- child component template -->
<p class="foo bar">Hi!</p>
```
Then add some classes when using it:
```
<!-- when using the component -->
<MyComponent class="baz boo" />
```
The rendered result will be:
```
<p class="foo bar baz boo">Hi</p>
```
This is also the case with class Bindings
If the component has multiple root elements, one needs to specify which of the root elements will receive the class using the `$attrs` component property:
```
<!-- MyComponent template using $attrs -->
<p :class="$attrs.class">Hi!</p>
<span>This is a child component</span>
```
and:
```
<MyComponent class="baz" />
```
will render:
```
<p class="baz">Hi!</p>
<span>This is a child component</span>
```



## Binding Inline styles:

### Binding to Objects:
`:style` supports binding to JS object values. It corresponds to an HTML's style property.
```
data() {
  return {
    activeColor: 'red',
    fontSize: 30
  }
}
```
and:
```
<div :style="{ color: activeColor, fontSize: fontSize + 'px' }"></div>
```
Although camel case is recommended, vue also supports conventional kebab-case CSS.ie:
```
<div :style="{ 'font-size': fontSize + 'px' }"></div>
```
It is however recommended, for a cleaner looking template, to bind to a style object directly:
```
data() {
  return {
    styleObject: {
      color: 'red',
      fontSize: '13px'
    }
  }
}
```
and: 
```
<div :style="styleObject"></div>
```
### Binding to Arrays:
These objects will be merged and applied to the same element
```
<div :style="[baseStyles, overridingStyles]"></div>
```
### Auto Prefixing:
For CSS properties that require a vendor prefix, vue automatically adds them. 

### Multiple Values:
```
<div :style="{ display: ['-webkit-box', '-ms-flexbox', 'flex'] }"></div>
```
This will render the last value in the array that the browser supports.

## Conditional Rendering:
### v-ifand v-else:
Used to conditionally render a block:

```
<button @click="awesome = !awesome">Toggle</button>

<h1 v-if="awesome">Vue is awesome!</h1>
<h1 v-else>Oh no 😢</h1>
```
### v-else-if:
```
<div v-if="type === 'A'">
  A
</div>
<div v-else-if="type === 'B'">
  B
</div>
<div v-else-if="type === 'C'">
  C
</div>
<div v-else>
  Not A/B/C
</div>
```
These directives can also be used on `<template>` but will not be rendered in the final result.

### v-show:
Similar to `v-if`, the difference being that it the element is rendered but not displayed by toggling the `display` property in CSS.
It also doesnt support the `<template>`  element neither does it support `v-else`
`v-if` is lazy, it will not render at all if the condition is false in the first render.
`v-if` has higher toggle costs...while `v-show` 
has higher initial render costs.


## List Rendering:

### v-for:
Used to render a list of items based on an array.
```
data() {
  return {
    items: [{ message: 'Foo' }, { message: 'Bar' }]
  }
}
```
and:
```
<li v-for="item in items">
  {{ item.message }}
</li>
```
`v-for` also supports an optional second alias for the index of the current item.
```
data() {
  return {
    parentMessage: 'Parent',
    items: [{ message: 'Foo' }, { message: 'Bar' }]
  }
}
```
and:
```
<li v-for="(item, index) in items">
  {{ parentMessage }} - {{ index }} - {{ item.message }}
</li>
```
The `v-for` scope has access to parent scopes.
```
<li v-for="item in items">
  <span v-for="childItem in item.children">
    {{ item.message }} {{ childItem }}
  </span>
</li>
```
Note that `of` can be used instead of `in`. Also, `v-for` works with objects
```
<li v-for="(value, key, index) in myObject">
  {{ index }}. {{ key }}: {{ value }}
</li>
```
### v-for with a range:
```
<span v-for="n in 10">{{ n }}</span>
```
Note that `n` in this case begins from 1, not 0

### v-for on `<template>`:
```
<ul>
  <template v-for
  ="item in items">
    <li>{{ item.msg }}</li>
    <li class="divider" role="presentation"></li>
  </template>
</ul>
```
### v-for with v-if:
If used on the same node, `v-if` has a higher priority. This is solved by:
```
<template v-for="todo in todos">
  <li v-if="!todo.isComplete">
    {{ todo.name }}
  </li>
</template>
```
 ### Maintaining state with key:
 While vue is updating a list of elements with `v-for`, by default, it uses an 'in-place' patch strategy. If the order of items has changed, instead of moving the DOM elements to match the order of items, vue will patch each elements in place and make sure it reflects what should be rendered at that specific index. 
 However, this is only suitable when the list render output does not rely on child component state or temporary DOM state.(eg, form input values)
 for vue to track each node's identity, one needs to provide a unique key attibute for each item:
 ```
 <div v-for="item in items" :key="item.id">
  <!-- content -->
</div
```
In a template element, the key should be placed on the `<template>` container.
The key binding expects primitive values, strings and numbers, not objects.

### v-for with a component:
```
<MyComponent v-for="item in items" :key="item.id" />
```
One must remember to provide a `key` however. 
This will however, not pass any data to the component, because component have isolated scopes of their own. to pass data, we use props:
```
<MyComponent
  v-for="(item, index) in items"
  :item="item"
  :index="index"
  :key="item.id"
/>
```

### Array Change Detection:
vue is able to detect when a reactive array's methods are called and trigger necessary updates. 

### Replacing an array:
There are also non-mutating methods such as `filter()`, `concat()` which return new arrays. 
When working with these, we should always replace the old array with the new one:
```
this.items = this.items.filter((item) => item.message.match(/Foo/))
```
Vue provides smart heuristics to maximize DOM element use, hence the entire DOM is not thrown away.

### Displaying sorted of filtered data:
To do this, one may not want to replace the entire array, instead, one should create a computed property that returns the filtered or sorted array:
```
data() {
  return {
    numbers: [1, 2, 3, 4, 5]
  }
},
computed: {
  evenNumbers() {
    return this.numbers.filter(n => n % 2 === 0)
  }
}
```
and:
```
<li v-for="n in evenNumbers">{{ n }}</li>
```

In the case where computed properties are not possible like in nested loops, one can use a method:
```
data() {
  return {
    sets: [[ 1, 2, 3, 4, 5 ], [6, 7, 8, 9, 10]]
  }
},
methods: {
  even(numbers) {
    return numbers.filter(number => number % 2 === 0)
  }
}
```
and:
```
<ul v-for="numbers in sets">
  <li v-for="n in even(numbers)">{{ n }}</li>
</ul>
```
One should avoid mutative methods like `reversed()` in a computed property. one can create a copy before calling the methods.

### Event Handling:

We can use the `v-on` directive or the `@:attribute = ""` shorthand. The handler could be inline or a method handler.

```
data() {
  return {
    name: 'Vue.js'
  }
},
methods: {
  greet(event) {
    // `this` inside methods points to the current active instance
    alert(`Hello ${this.name}!`)
    // `event` is the native DOM event
    if (event) {
      alert(event.target.tagName)
    }
  }
}
``` 
and:
```
<button @click="greet">Greet</button>

```
### Calling methods in inline handlers:

We can also call methods in an inline manner:
```
methods: {
  say(message) {
    alert(message)
  }
}
```
and:
```
<button @click="say('hello')">Say hello</button>
<button @click="say('bye')">Say bye</button>
```

### Accessing event Argument in inline handlers:
Sometimes, we need to access the original DOM event in an inline handler. It can be passed into a method using the special `$event` variable, or use an arrow function:
```
<!-- using $event special variable -->
<button @click="warn('Form cannot be submitted yet.', $event)">
  Submit
</button>

<!-- using inline arrow function -->
<button @click="(event) => warn('Form cannot be submitted yet.', event)">
  Submit
</button>
```
and:
```
methods: {
  warn(message, event) {
    // now we have access to the native event
    if (event) {
      event.preventDefault()
    }
    alert(message)
  }
}
```
### Event Modifiers:
Include:

1. .stop
2. .prevent
3. .self 
4. .capture 
5. .once 
6. .passive 
```
<!-- the click event's propagation will be stopped -->
<a @click.stop="doThis"></a>

<!-- the submit event will no longer reload the page -->
<form @submit.prevent="onSubmit"></form>

<!-- modifiers can be chained -->
<a @click.stop.prevent="doThat"></a>

<!-- just the modifier -->
<form @submit.prevent></form>

<!-- only trigger handler if event.target is the element itself -->
<!-- i.e. not from a child element -->
<div @click.self="doThat">...</div>
```
Note that order also matters. 
```
<!-- use capture mode when adding the event listener -->
<!-- i.e. an event targeting an inner element is handled here before being handled by that element -->
<div @click.capture="doThis">...</div>

<!-- the click event will be triggered at most once -->
<a @click.once="doThis"></a>

<!-- the scroll event's default behavior (scrolling) will happen -->
<!-- immediately, instead of waiting for `onScroll` to complete  -->
<!-- in case it contains `event.preventDefault()`                -->
<div @scroll.passive="onScroll">...</div>
```
### Key Modifiers:
```
<!-- only call `vm.submit()` when the `key` is `Enter` -->
<input @keyup.enter="submit" />
```
One can directly use key names exposed via `keyBoardEvent.key` as modifiers by converting them to kebab-case.
```
<input @keyup.page-down="onPageDown" />
```
In th above example, the handler will only be called if `$event.key` is equal to `PageDown`
There are many key and moust button modifiers as well.

## Form Input Bindings:

When dealing with forms, we often need to sync the state of form input elements with the corresponding state in js. It us cumbersome to write up value bindings and eventlisteners:
```
<input
  :value="text"
  @input="event => text = event.target.value">
```
the `v-model` directive simplifies the above to:
```
<input v-model="text">
```
In addition,`v-model` can be used on inputs of different types, `<textarea>` and `<select>` elements.
It automatically expands to different DOM property and event pairs based on the elements it is used on:

1. `input` with `text` type and `textarea` use `value` property and `input` event.
2. `input` of type `checkbox` and `radio` use `checked` property and `change` event.
3. `<select>` use `value` as a prop and `change` as and event.

Note that `v-model` will ignore the initial values of the attributes as the bound js state is treated as the source of truth. The initial value should be declared using the `data` option.

### Multiple checkboxes:
One can also bind multiple checkboxes to the same array or set value:
```
export default {
  data() {
    return {
      checkedNames: []
    }
  }
}
```
and:
```
<div>Checked names: {{ checkedNames }}</div>

<input type="checkbox" id="jack" value="Jack" v-model="checkedNames">
<label for="jack">Jack</label>

<input type="checkbox" id="john" value="John" v-model="checkedNames">
<label for="john">John</label>

<input type="checkbox" id="mike" value="Mike" v-model="checkedNames">
<label for="mike">Mike</label>
```

### Select:
Single select:
```
<div>Selected: {{ selected }}</div>

<select v-model="selected">
  <option disabled value="">Please select one</option>
  <option>A</option>
  <option>B</option>
  <option>C</option>
</select>
```
Multiple select, bound to array:
```
<div>Selected: {{ selected }}</div>

<select v-model="selected" multiple>
  <option>A</option>
  <option>B</option>
  <option>C</option>
</select>
```
Note that select options can be dynamically rendered with `v-for`:
```
export default {
  data() {
    return {
      selected: 'A',
      options: [
        { text: 'One', value: 'A' },
        { text: 'Two', value: 'B' },
        { text: 'Three', value: 'C' }
      ]
    }
  }
}
```
and:
```
<select v-model="selected">
  <option v-for="option in options" :value="option.value">
    {{ option.text }}
  </option>
</select>

<div>Selected: {{ selected }}</div>
```
### Value bindings:
```
<!-- `picked` is a string "a" when checked -->
<input type="radio" v-model="picked" value="a" />

<!-- `toggle` is either true or false -->
<input type="checkbox" v-model="toggle" />

<!-- `selected` is a string "abc" when the first option is selected -->
<select v-model="selected">
  <option value="abc">ABC</option>
</select>
```
We may want to bind to a dynamic property on the current active instance:
```
<input
  type="checkbox"
  v-model="toggle"
  true-value="yes"
  false-value="no" />
  ```

  Here, `true-value` and `false-value` are vue-specific attributes that only work with `v-model`. One can also bind to dynamic values using `v-bind`:
  ```
  <input
  type="checkbox"
  v-model="toggle"
  :true-value="dynamicTrueValue"
  :false-value="dynamicFalseValue" />
  ```
  For radio buttons:
  ```
  <input type="radio" v-model="pick" :value="first" />
  <input type="radio" v-model="pick" :value="second" />
```
`v-model` supports value bindings of non-string values, such as objects:
```
<select v-model="selected">
  <!-- inline object literal -->
  <option :value="{ number: 123 }">123</option>
</select>
```
### Modifiers:
.lazy:<br>
By default, `v-model` syncs input with the data after each `input` event. the lazy modifier changes this to sync on `change` events.
```
<!-- synced after "change" instead of "input" -->
<input v-model.lazy="msg" />
```
.number: <br>
Typecasts the input as a number.
If it cannot be parsed using `parseFloat()`, the original value is used instead.
.trim: <br>
Removes all whitespace from the input.

## Lifecycle Hooks:

Every vue component undergoes through a series of initialization steps when created like setting up data observation, compilation of the template, mounting of the instance to the DOM, and updating the DOM when data changes. Along the way, it runs functions called lifecyle hooks, giving users the opportunity to add their own code at specific stages:

### Registering Lifecycle Hooks:
The `mounted` hook can be used to run code after the component has finished intial rendering and created DOM nodes. Other common hooks include `unmounted` and `updated`.All lifecycle hooks are called with the `this` context pointing to the current active instance. Therefore, avoid using arrow functions since you will be unable to access the component instance.

## Watchers:
Sometimes, we need to perform 'side effects' in response to state changes. with the options API, we can use the `watch`option to trigger a function whenever a reactive property changes:
```
export default {
  data() {
    return {
      question: '',
      answer: 'Questions usually contain a question mark. ;-)'
    }
  },
  watch: {
    // whenever question changes, this function will run
    question(newQuestion, oldQuestion) {
      if (newQuestion.includes('?')) {
        this.getAnswer()
      }
    }
  },
  methods: {
    async getAnswer() {
      this.answer = 'Thinking...'
      try {
        const res = await fetch('https://yesno.wtf/api')
        this.answer = (await res.json()).answer
      } catch (error) {
        this.answer = 'Error! Could not reach the API. ' + error
      }
    }
  }
}
```
and:
```

<p>
  Ask a yes/no question:
  <input v-model="question" />
</p>
<p>{{ answer }}</p>
```

Note that the `watch` element supports a dot delimited path as the key.

### Deep Watchers:

Watch is shallow by default as it will only trigger if the watched property has been assigned to a new value. It will not trigger on nested property changes. This is where deep watches come in:
```
export default {
  watch: {
    someObject: {
      handler(newValue, oldValue) {
        // Note: `newValue` will be equal to `oldValue` here
        // on nested mutations as long as the object itself
        // hasn't been replaced.
      },
      deep: true
    }
  }
}
```
They are however very expensive when used on large data structures hence are to be used with caution.

### Eager Watchers:
`watch` is lazy by default. It will not be called until the watched source has changed.
We can force a watcher's callback to be executed immediately by declaring using an object with an handler function and the `immediate: true` option.
```
export default {
  // ...
  watch: {
    question: {
      handler(newQuestion) {
        // this will be run immediately on component creation.
      },
      // force eager callback execution
      immediate: true
    }
  }
  // ...
}
```
### Callback Flush Timing:

When a reactive state mutates, one triggers both vue component updates and watcher callbacks. This means that if one attempts to access the DOM inside a watcher callback, it would still be in its pre-updated state. If one wants to access the DOM after vue has updated it, one needs to specify the `flush: post` option

One can also create watchers imperatively using the `$watch()` instance method. 
```
export default {
  created() {
    this.$watch('question', (newQuestion) => {
      // ...
    })
  }
}
```
This is useful when one wants to conditionally set up a watcher, or stop a watcher early.

### Stopping a watcher:
All watchers are automatically stopped when their owner components are unmounted. In the event one needs to stop a watcher:
```
const unwatch = this.$watch('foo', callback)

// ...when the watcher is no longer needed:
unwatch()
```

## Template Refs:

Vue's declarative rendering model abstracts away most of the away most of the direct DOM operations, one may still need to access the underlying DOM elements. To do this, one can use the special `ref` attribute.
```
<input ref="input">
```
### Accessing the Refs:

```
<script>
export default {
  mounted() {
    this.$refs.input.focus()
  }
}
</script>

<template>
  <input ref="input" />
</template>
```
Note that one can only access the `refs` only after the component is mounted. It is therefore null in a template expression on the first render. 

### Refs inside v-for:
when used inside `v-for`, the result is an array containing the corresponding elements
```
<script>
export default {
  data() {
    return {
      list: [
        /* ... */
      ]
    }
  },
  mounted() {
    console.log(this.$refs.items)
  }
}
</script>

<template>
  <ul>
    <li v-for="item in list" ref="items">
      {{ item }}
    </li>
  </ul>
</template>
```

### Function Refs:
Instead of a string key, `ref` can also be bound to a function which will be called on each component update. The element reference is received as the first argument:

```
<input :ref="(el) => { /* assign el to a property or ref */ }">
```
Note that we are using a dynamic `:ref` binding. The argument is `null` when the element is unmounted.

### Ref on Component:
`ref` can also be used on a child component.In this case, the ref will be that of the component instance. 
```
<script>
import Child from './Child.vue'

export default {
  components: {
    Child
  },
  mounted() {
    // this.$refs.child will hold an instance of <Child />
  }
}
</script>

<template>
  <Child ref="child" />
</template>
```
The referenced instance will be equal to the child component's `this` which means the parent will have full access to the child's methods and properties. 

The `expose` option can be used to limit access to a child's instance. 
```
export default {
  expose: ['publicData', 'publicMethod'],
  data() {
    return {
      publicData: 'foo',
      privateData: 'bar'
    }
  },
  methods: {
    publicMethod() {
      /* ... */
    },
    privateMethod() {
      /* ... */
    }
  }
}
```
In the above, a parent referencing this component will only have access to `publicData` and `publicMethod`

## Components:


