<template>
<div>
  <header> ToDo App</header>
  <div>
    <h3>Todo Items</h3>
    <ul v-if="todos.length > 0">
      <li :key="index" v-for="(todo, index) in todos">
        <input type="checkbox" v-model="todo.completed" @click="toggleTodo(index, 'todos')" />
        {{todo.text}}
        <span @click= "deleteTodo(index)">X</span>
      </li>
    </ul>
    <span v-else>No items in the list</span>
  </div>
  <div>
    <h3>Completed Items</h3>
    <ul v-if="completed.length > 0">
      <li :key="index" v-for="(todo, index) in completed">
        <input type="checkbox" v-model="todo.completed" @click="toggleTodo(index, 'completed')" />
        {{todo.text}}
      </li>
    </ul>
    <span v-else>No Items in the list</span>
  </div>
  <div>
    <h3>Add a new Item</h3>
      <input type="text" v-model="input" @keyup.enter="addTodo"/>
      <button @click="addTodo"> Add Item</button>
  </div>
</div>
</template>

<script>
export default {
  name: "Todos",
  data() {
    return {
      todos : [{
        text: "Buy groceries",
        completed: false
      }],
      completed: [],
      input:""
    };
  },

  methods: {
    addTodo: function(){
      if(this.input !== ""){
        let newTodo = {
          text: this.input,
          completed: false
        }
        this.todos.push(newTodo);
        this.input=""
      }
    },
    deleteTodo: function(index){
      this.todos.splice(index, 1);
    },
    toggleTodo: function(index, listname){
      if(listname === "todos") {
        this.completed.push(this.todos[index]);
        this.todos.splice(index,1);
      } else {
        this.todos.push(this.completed[index]);
        this.completed.splice(index,1);
      }
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
header{
  font-weight: normal;
  text-align : center
}
ul {
  list-style-type: none;
  padding: 0;
}
li,
form,
button,
span {
  display: inline-block;
  margin: 0 10px;
}
li {
  display: block;
  margin: 0 10px;
}
</style>
