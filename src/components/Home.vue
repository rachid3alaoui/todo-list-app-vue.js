<template>
  <div>
    <header>
      <h1> {{ title }}</h1>
    </header>
    
    <form>
      <input type="text" class="todo-input" v-model="todoInput">
      <button class="todo-button" type="submit" v-on:click.prevent="addTodo">
        <i class="fas fa-plus-square"></i>
      </button>
      <div class="select">
        <select name="todos" v-model="selected">
          <option value="all">All</option>
          <option value="completed">Completed</option>
          <option value="uncompleted">Uncompleted</option>
        </select>
      </div>
    </form>

    <div class="todo-container">
      <ul class="todo-list">
        <div v-for="todo in getTodos" :key="todo.id" class="todo" :class="{completed: todo.completed, deleted: todo.deleted}">
          <li>{{ todo.content }}</li>
          <span><i class="fas fa-check" @click="markAsCompleted(todo.id)"></i></span>
          <span><i class="fas fa-trash" @click="deleteTodo(todo.id)"></i></span>
        </div>
      </ul>
    </div>
  </div>
</template>

<script>
import {v4 as uuidv4} from "uuid";

export default {
  name: 'Home',
  data() {
    return {
      title : "Rachid's Todo List",
      todos : [],
      todoInput : "",
      selected : null,
    }
  },
  computed : {
    getTodos(){
      if(this.selected === "uncompleted"){
        return this.todos.filter(todo => todo.completed === false);
      } else if (this.selected === "completed"){
        return this.todos.filter(todo => todo.completed)
      } else {
        return this.todos;
      }
    }
  },
  methods : {
    addTodo(){
      if(this.todoInput.trim() !== ""){
        this.todos.push(
          {id: uuidv4(), content: this.todoInput.trim(), completed: false, deleted : false}
        );
      } else {
        alert('Please fill in the form');
      }
      this.todoInput = "";
    },
    deleteTodo(id){
      this.todos.map(todo => todo.id === id ? todo.deleted = !todo.deleted : todo.deleted)
      setTimeout(() => {
        this.todos = this.todos.filter(todo => {
        return todo.id !== id;
      })
      }, 500)
    },
    markAsCompleted(id){
      this.todos.map(todo => {
        if(todo.id === id) {
          todo.completed = !todo.completed;
        }
      })
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
header {
  font-size: 2rem;
}


header, form {
  min-height:20vh;
  display: flex;
  justify-content: center;
  align-items: center;
  
}

form input, form button {
  padding: 0.5rem;
  font-size: 2rem;
  border: none;
  background: white
}

form input[type="text"] {
  box-shadow: rgba(0, 0, 0, 0.15) 1.95px 1.95px 2.6px;
  margin-right: 0.5rem;
  border-radius: 0.4rem;
}

form button {
  color: #ff6f47;
  background: #f7fffe;
  box-shadow: rgba(0, 0, 0, 0.15) 1.95px 1.95px 2.6px;
  border-radius: 0.4rem;
  margin-right:0.5rem;
  cursor: pointer;
  transition: all 0.3s ease;
}

form button:hover {
  background: #ff6f47;
  color: #f7fffe;
}

.todo-container {
  display: flex;
  justify-content: center;
  align-items: center;
}

.todo-list {
  min-width: 30%;
  list-style: none;
}

.todo {
  width: 100%;
  display: flex;
  justify-content: space-between;
  align-items: center;
  background-color: #fff;
  color: #000;
  margin: 0.5rem;
  padding: 0.5rem;
  border-radius: 0.2rem;
  box-shadow: rgba(0, 0, 0, 0.15) 1.95px 1.95px 2.6px;
  font-size: 1.5rem;
  transition: all 0.7s ease;  
}

.todo li {
  flex: 1;
}

.fa-trash, .fa-check {
  padding: 0rem 0.2rem;
  cursor: pointer;
  transition: all 0.6s ease;
}

.fa-trash:hover , .fa-trash:hover {
  opacity: 0.7;
}

.fa-trash {
  color: red;
}

.fa-check {
  color: green;
  margin-right: 0.2rem;
}

.select {
  position: relative;
  overflow: hidden;
}

select {
  color: #ff6f47;
  cursor: pointer;
  width: 12rem;
  padding: 1rem 0;
  border: none;
  color: black;
  border-radius: 0.4rem;
}

.completed {
  text-decoration: line-through;
  opacity: 0.5;
}

.deleted {
  transform: translateX(20rem);
  opacity: 0;
}

</style>
