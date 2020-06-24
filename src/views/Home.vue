<template>
  <div id="app">
    <AddTodo @add-todo = 'addTodo'></AddTodo>
    <div class='error'>
      <p>{{errorMessage}}</p>
    </div>
    <Todos :todos='todos' @del-todo='deleteTodo'></Todos>
  </div>
</template>

<script>
import axios from 'axios';

import AddTodo  from '../components/AddTodo';
import Todos  from '../components/Todos';

export default {
  name: 'Home',
  components: {
    AddTodo,
    Todos,
  },
  data() {
    return {
      todos: [],
      errorMessage: null
    }
  },
  methods: {
    deleteTodo(id) {
      // axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
      //   .then(this.todos = this.todos.filter(item => item.id !== id))
      //   .catch(err => console.log(err));
      this.todos = this.todos.filter(item => item.id !== id)
    },
    addTodo (newTodo) {
      const {title, completed} = newTodo;
      if(title === '') {
        this.errorMessage = 'This field must not be empty';
        return false;
        }
      //my solution, because json.placeholder send only 201 id
      // let i = this.todos[this.todos.length - 1].id;
      let i = (this.todos.length === 0) ? i = 1 : this.todos[this.todos.length - 1].id;
      this.todos.push({
            id:  i += 1, 
            title, 
            completed });
      this.errorMessage = null;

      // axios.post('https://jsonplaceholder.typicode.com/todos', {
      //     title,
      //     completed,
      //   })
      //   .then(res => this.todos = [...this.todos, res.data])
      //   .catch(err => console.log(err));
    }
  },
  created() {
      axios.get('https://jsonplaceholder.typicode.com/todos?_limit=5')
        .then(res => this.todos = res.data)
        .catch(err => console.log(err));
    }
}
</script>

<style>
  * {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
  }
  body {
    font-family: Arial, Helvetica, sans-serif;
    line-height: 1.4;
  }
  .btn {
    display: inline-block;
    border: none;
    background: #555;
    color: #fff;
    padding: 7px 20px;
    cursor: pointer;
  }
  .btn:hover {
    background: #666;
  }
  .error {
    color: red;
  }
</style>
