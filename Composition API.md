links: [[VUE - 3]], [[000 Index]]
tags: 

-----------
[[Vue-3-Composition-Cheat-Sheet.pdf]]




Composition API is more readable
- organized by logical concerns
- optimal TS support
To make reactive items accessible by the template we use the setup() function
`setup` executes before any of these options:
- Components
- Props
- Data
- Methods
- Computed Properties
- Lifecycle methods
`setup` cannot access `this` modifier

`setup` has two optional arguments
```ts
import { watch } from "vue"; 
export default { 
	props: { 
		name: String 
	}, 
	setup(props) { 
		watch(() => {
			console.log(props.name);
			}); 
		} 
	};
```
the second argument is context, that has a bunch of useful data;
```ts
setup(props, context) { 
	context.attrs; 
	context.slots;
	context.parent; 
	context.root; 
	context.emit; 
}
```

inside the setup the return data is what is needed to expose data to the renderContext

`<suspense>` component that allows you to wait for any asynchronous work to complete before a component is displayed
built in component that we can use to wrap two different templates, like so:
```TS
<template> 
	<Suspense> 
		<template #default> 
			<!-- Put component/components here, one or more of which makes an asychronous call --> 
		</template> 
		<template #fallback> 
			<!-- What to display when loading --> 
		</template> 
	</Suspense> 
</template>
```

When `suspense` loads it will first attempt to render out what it finds in `<template #default>`. If at any point it finds a component with a `setup` function that returns a promise, or an Asynchronous Component (which is a new feature of Vue 3) it will instead render the `<template #fallback>` until all promises have been resolved

```TS
<template>
  <Suspense>
    <template #default>
      <Event />
    </template>
    <template #fallback>
      Loading...
    </template>
  </Suspense>
</template>
<script>
import Event from "@/components/Event.vue";
export default {
  components: { Event },
};
</script>
```

suspense will wait for all asynchronous calls to finish before loading the template even if the call are deeply nested component

displaying an error screen can be used through v-if, and we have `onErrorCaptured` lifecycle hook that we can use to listen for errors:
```ts
<template>
  <div v-if="error">Uh oh .. {{ error }}</div>
  <Suspense v-else>
    <template #default>
      <Event />
    </template>
    <template #fallback>
      Loading...
    </template>
  </Suspense>
</template>
<script>
import Event from "@/components/Event.vue";
import { ref, onErrorCaptured } from "vue";
export default {
  components: { Event },
  setup() {
    const error = ref(null);
    onErrorCaptured((e) => {
      error.value = e;
      return true;
    });
    return { error };
  },
};
</script>
```

skeleton loading screens would go into your `<template #fallback>` and your rendered HTML would go into your `<template #default>`