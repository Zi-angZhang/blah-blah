# a tutorial of vue.js

At the core of Vue.js is a system that enables us to declaratively render data to the __DOM__ using straight forward template syntax:

``` vue
<div id='app'>
    {{message}}
</div>

vue app = new Vue({
    el: '#app',
    data:{
        message:'Hellow vue!'
    }
})

```

> DOM (Document Object Model) connects web pages to scripts or programming languages by representing the structure of a document-such as the HTML representing a web page - in memory. 

`v-bind` attribute you are seeing is called a __directive__. `v-` means they are provided by _Vue_.

```vue
<div id='app-2'>
    <span v-bind:title='message'>
    Hover your mouse over me for a few seconds
    </span>
</div>
var app2 = new Vue({
	el: '#app-2',
	data:{
		message: new Data().toLocalString()
	}
})
```

``` html
<div id="app-3">
  <span v-if="seen">Now you see me</span>
</div>
<script>
	var app3 = new Vue({
        el: '#app3',
        data:{
            seen: true
        }
    })
</script>

```

var 50