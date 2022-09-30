<template>
  <div id="app">
    <h1>vue-TodoList</h1>
    <input 
      type="text" 
      @keyup.enter="addTodo"
      v-model="todoText"
    />

    <hr>

    <todoList 
      v-for="todo in todos" 
      :key="todo.id" 
      :todo="todo" 
      @todo-Check="checkChange"
      @todo-del="todoDel"
    />
    
  </div>
</template>

<script>
import todoList from './components/todoList.vue'
export default {
  components: {
    todoList
  },
  data() { 
    return {
      todoText: '',
      todos: [
        { id: 1, text: "text1", checked: false },
        { id: 2, text: "text2", checked: false }
      ]
    }
  },
  methods: {
    addTodo(e){
      this.todos.push({
        id: Math.random(),
        text: e.target.value,
        checked: false
      });

      this.todoText = '';
    },
    checkChange({id, checked}){
      const index = this.todos.findIndex(todo => {
        return todo.id == id;
      });

      this.todos[index].checked = checked;
    },
    todoDel({id}){
      // const index = this.todos.findIndex(todo => {
      //   return todo.id == id;
      // });

      // this.todos.splice(index, 1);
      this.todos = this.todos.filter(todo => todo.id !== id);
    }
  }
}
</script>

<style>
body{
  background: mintcream;
}
#app {
  width: 500px;
  padding: 10px 20px 50px 20px;
  margin: 0 auto;
  background: #fff;
}
#app>input{
  width: 50%;
  margin-bottom: 10px;
}
</style>
