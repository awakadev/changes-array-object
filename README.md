

### What are the caveats of array changes detection?
Vue cannot detect changes for the array in the below two cases,

1. When you directly set an item with the index,For example,
   ```javascript
   vm.tods[indexOfTodo] = newTodo
   ```
2. When you modify the length of the array, For example,
 ```javascript
 vm.todos.length = todosLength
 ```
You can overcome both the caveats using `set` and `splice` methods, Let's see the solutions with an examples,
**First use case solution**
```javascript
// Vue.set
Vue.set(vm.todos, indexOfTodo, newTodoValue)
(or)
// Array.prototype.splice
vm.todos.splice(indexOfTodo, 1, newTodoValue)
```
**Second use case solution**
```javascript
vm.todos.splice(todosLength)
```
### What are the caveats of object changes detection?
Vue cannot detect changes for the object in property addition or deletion., Lets take an example of user data changes,
```javascript
var vm = new Vue({
  data: {
    user: {
      name: 'John'
    }
  }
})

// `vm.name` is now reactive

vm.email = john@email.com // `vm.email` is NOT reactive
```
You can overcome this scenario using the Vue.set(object, key, value) method or Object.assign(),
```javascript
Vue.set(vm.user, 'email', john@email.com);
(or)
vm.user = Object.assign({}, vm.user, {
  email: john@email.com
})
```
