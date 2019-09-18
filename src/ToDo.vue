<template>
  <div id="app">
    <div class="ToDo">
      <img :src="logo" alt="Vue Logo" class="Logo">
      <h1 class="Todo-Header">Vue To Do</h1>
      <div class="ToDo-Container">
        <ToDoItem v-for="todo in list"
          :todo="todo"
          @delete="onDeleteItem"
          :key="todo.id" />
      </div>
      <input type="text" v-model="todo" @keyup.enter="createToDoItem">
      <button class="ToDo-Add" @click="createToDoItem()">+</button>
    </div>
  </div>
</template>

<script>
import ToDoItem from './components/TodoItem';
import Logo from './assets/logo.png';
export default {
  name: 'to-do',
  components: {
    ToDoItem
  },
  data() {
    return {
      list: [
        {
          id: 1,
          text: 'clean the house'
        },
        {
          id: 2,
          text: 'buy milk'
        }
      ],
      todo: '',
      logo: Logo
    }
  },
  methods: {
    createToDoItem() {
      if (!this.todo) {
        alert('Please enter a todo!');
        return;
      }

      const newId = Math.max.apply(null, this.list.map(t => t.id)) + 1;
      this.list.push({ id: newId, text: this.todo });
      this.todo = '';
    },
    onDeleteItem(todo) {
      this.list = this.list.filter(item => item !== todo);
    }
  }
}
</script>

<style>
  body {
  margin: 0;
  padding: 0;
  font-family: -apple-system, BlinkMacSystemFont, Helvetica Neue, Helvetica, Arial, sans-serif;
  background: linear-gradient(#aeffae, #3d99ff);
  height: auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
}

.Logo {
  width: 50px;
  position: relative;
  top: 50px;
}

.ToDo {
  text-align: center;
  border: 1px solid white;
  width: 80vw;
  height: auto;
  box-shadow: 2px 3px 15px rgba(0, 0, 0, 0.5);
  background: #f6f6f6;
  padding-bottom: 60px;
  margin: 40px auto;
}

.ToDo-Header {
  color: black;
  font-family: -apple-system, BlinkMacSystemFont, Helvetica Neue, Helvetica, Arial, sans-serif;
  font-weight: 400;
  text-transform: uppercase;
  margin: 70px auto 30px;
}

.ToDo-Add {
  color: white;
  font-size: 2em;
  width: 40px;
  height: 40px;
  padding: 0px;
  display: flex;
  justify-content: center;
  align-items: center;
  cursor: pointer;
  background: #73ff73;
  border-radius: 10px;
  box-shadow: 1px 1px 1px #47a947;
  margin: 20px auto 0;
}

.ToDo-Add:hover {
  box-shadow: none;
  margin-left: calc(auto + 1px);
}

.ToDo-Container {
  width: 80%;
  margin: 0 auto;
}

input {
  width: 60%;
  padding: 10px;
  font-size: 1em;
  margin: 10px auto;
  box-shadow: 1px 3px 20px 0px rgba(0, 0, 0, 0.3)
}
</style>