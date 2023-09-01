links: [[VUE - 3]]
tags: #API

--------

[[#^8179bc|Pagination]]  
[[#^4f4647|Nested Routes]] 
[[#^47ba93|Programmatic Navigation]]
[[#^5b3dc8|Router Cheat Sheet]]


### `https://localhost:8080/events?page=4`
How to get access to a query value from the component
```js
$route.query.page
```

how to access to page inside our component
use a route parameter
/src/router/index.js
```jsx
const routes =[
	...
	{ path: '/events/:page', component: Events},
]

// to access in a component would look like this
<h1>You are on page {{ $route.params.page }}</h1>
```

to decouple the component from the route by telling our router to pass our param page as a component prop
```js
const routes = [ 
	... 
	{ path: '/events/:page', component: Events, props: true }, 
]
```
```html
inside the component
<template> 
	<h1>You are on page {{ page }}</h1> 
</template> 
<script> 
export default 
	{ props: ["page"] }; 
</script>
```

### Pagination
^8179bc

### Nested Routes
^4f4647

### Redirect and Alias
when the path gets longer it becomes necessary to redirect if your plan is to change the url


```ts
const routes = [ ... 
	{ path: '/events/:id', // <--- make plural 'events' 
	  name: 'EventLayout', 
	  ... 
	  }, 
	  { path: '/event/:id', redirect: to => { 
		  return { name: 'EventDetails', params: { id: to.params.id } } 
		  } 
	  },
```

to redirect a dynamic segment, we'll need to get access to the params when we create the new path


If you have multiple children from this event then you can create an array of children paths

```ts
{ 
	path: '/event/:id', redirect: () => { 
	return { name: 'EventDetails' } 
}, 
	children: [ 
	{ path: 'register', redirect: () => ({ name: 'EventRegister' }) }, 
	{ path: 'edit', redirect: () => ({ name: 'EventEdit' }) } ] 
},
```

Another way to solve this is by using the wildcard
```ts
{ 
	path: '/event/:afterEvent(.*)', redirect: to => { 
		return { path: '/events/' + to.params.afterEvent } } 
},
```

this is taking whatever comes after the matching word `/event/` and placing it after `/events/` 


### Programmatic Navigation

^47ba93

- Navigation is triggered using Vue Router when a `<router-link>` is clicked but can be triggered prgammatically
The solution: this.$router.push with the arguments the same as when we use router-link
```ts
<template>
  <p>Regstration form here</p>
  <button @click="register">Register Me!</button>
</template>
<script>
export default {
  props: ['event'],
  methods: {
    register() {
      // If registration API call is successful
      this.$router.push({
        name: 'EventDetails',
        params: { id: this.event.id }
      })
    }
  }
}
</script>
```

When you click on a `<router-link>` its simply calling the `$router.push` function inside the code. there are many different combinations 
```ts
// Directly to the path with a single string
this.$router.push('/about')

// Directly to the path with an object
this.$router.push({ path: '/about' })

// Directly to the named path
this.$router.push({ name: 'About' })

// With a dynamic segment as I showed above
this.$router.push({ name: 'EventDetails', params: { id: 3 } })

// With a query ... resulting in /?page=2 in our example app
this.$router.push({ name: 'EventList', query: { page: 2 } })
```

### Error Handling
- page that doesnt exist
- connectivity fails
- go to an event that doesn't exist


### Flash Messages


### In-Component Route Guards
beforeRouteEnter(routeTo, routeFrom, next) no `this` keyword
beforeRouteUpdate(routeTo, routeFrom, next)
beforeRouteLeave(routeTo, routeFrom, next)
- routeTo - refers to the route that is about to be navigated to
- routeFrom - refers to the route that is about to be navigated away from
- next- can be called in each of them to resolve the hook, and continue navigation

Use Vue Router Global Navigation Guards `beforeEach` and `afterEach` inside the router file
```ts
import NProgress from 'nprogress'
... 
router.beforeEach(() => { 
	NProgress.start() }) 
router.afterEach(() => { 
	NProgress.done() }) 

export default router
```


### Router Cheat Sheet
^5b3dc8
[[Vue-Router-Cheat-Sheet.pdf]] 
![[Vue-Router-Cheat-Sheet.pdf]]
