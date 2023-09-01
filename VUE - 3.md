links[[010 Technologies]], [[000 Index]]
tags: #vue

-------
[[Router API]] 
[[Composition API]] 

#### DOCS
----------------------------------
[[Router API Docs]]





Three modules of vue Core 
- Reactivity Module : create JS reactive objects that can be watched for changes
- Compiler Module : 
- Renderer Module :

**Virtual DOM:** completely decouples rendering logic from the actual DOM makes it straightforward to reuse it in non-browser environments, e.g. rendering to a string (SSR), rendering to canvas/WebGL, or native mobile rendering
- ability to programmatically construct, inspect, clone and create derivative structures using the full power of JS

**Server-Side Routing**  browser -> requests the app -> server returns the app and refreshes the entire page every time a new view is requested

**Client-Side Routing** browser -> request the app -> server sends the app as an index.html -> the router navigates around that single page component showing the different views. Without having to reload the page
> not always beneficial to send the total webpage upon initial load can use performance optimization 
```JS
component: () => import('../views/AboutView.vue')
```
This imports the webpage view only when it is requested. 