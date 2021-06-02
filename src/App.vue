<template>
  <div id="app" class="container">
    <h1 class="text-center">Todo App</h1>

    <CompletedTodo :todos="todos" />

    <AddTodo @add-todo="addTodo"/>

    <hr>

    <TodoList :todos="todos" 
       @toggle-checkbox="toggleCheckbox" 
       @click-delete="deleteTodo"
    />

   {{ todos }}
  </div>
</template>

<script>
import TodoList from '@/components/TodoList';
import AddTodo from '@/components/AddTodo';
import CompletedTodo from '@/components/CompletedTodo';

export default {
  components: {
    TodoList,
    AddTodo,
    CompletedTodo
  },
  data() {
    return {
      todos: [
        { id: 1, text: 'buy a car', checked: false},
        { id: 2, text: 'play game', checked: false}
      ]
    }
  },

  methods: {
    deleteTodo(id) {
      //방법1
      // const index = this.todos.findIndex(todo => {
      //   return todo.id === id;
      // });
      // this.todos.splice(index, 1);

      //방법2
      this.todos = this.todos.filter(todo => todo.id !== id);
    },
    addTodo(value) {
        //입력창에 쓴 글자를 나타낼수 있다.
        console.log(value)
        //오브젝트를 todos에다가 push
        this.todos.push({
          id: Math.random(),
          text: value,
          checked: false
        });
       
    },
    //보낸 값 {}괄호를 통해 원하는 값을 바로 출력가능
    toggleCheckbox({id, checked}) {
      console.log(id,checked);
      const index = this.todos.findIndex(todo => {
        return todo.id === id;
      });
      this.todos[index].checked = checked;

    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
