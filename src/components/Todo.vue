<template>
  <div class="app-section">
    <div class="add">
      <h1> Add Project Todo</h1>
      <button @click="toggleForm" class="btn">+</button>

      <Form @add-todos="addTodos" v-if="showForm" :method='toggleForm' />
    </div>
    <div>
      <h1 class="h1">Todo List</h1>
      <div class="list">
        <div   v-for="(todo, index) in todos" :key="index">
          <div :class="todo.isChecked ? 'each' : 'n-each' ">
          <div>
          <span class="cancel" @click="onDelete(todo.title)"> X </span>
          <input @change="checkedEach(todo)" :checked='todo.isChecked'  class="check" type="checkbox" name="todo" id="todo" />
          </div>
          <h2 :for="todo.id" >{{ todo.title }}</h2>
          <h3>{{ todo.subTitle }}</h3>
          <p>{{ todo.description }}</p>
        </div>
      </div>
      </div>
    </div>
  </div>
</template>
<script>
import Form from "./Form.vue";
export default {
  name: "TodoApp",
  components: {
    Form,
  },
  data() {
    return {
      showForm: false,
      todos: [
        { id: 1,
          title: "Twitter Project",
          subTitle: " with React",
          description:
            " Build a twitter clone with neccesary functionalities use any storage means to store posts, mogodb advisable",
             isChecked: false,
       },
      ],
    };
  },
  methods: {
    toggleForm() {
      this.showForm = !this.showForm;
    },
    checkedEach(id) {
     if(id.isChecked === false){
       alert('Yahhh💃💃💃💃!!! one task completed')
     }
     else{
       alert('Ooops!!! one task not completed')
     }
      id.isChecked = !id.isChecked;
      // console.log("---->" , this.isChecked)
      
    },
    addTodos(todo) {
      // this.todos.push(todo);
      this.todos=this.todo=[...this.todos, {id: this.todos.length + 1, title: todo.title, subTitle: todo.subTitle, description: todo.description, isChecked: false}]
    },
    onDelete(title) {
      if(confirm("Are you sure you want to delete this todo?")) {
        this.todos = this.todos.filter((todo) => todo.title !== title);
      }
    },
    set(){
    if(localStorage.getItem('todos')){
      this.todos = JSON.parse(localStorage.getItem('todos'))
    }},
  },
  watch:{
    todos:{
      handler(){
        console.log(">>", this.todos)
        localStorage.setItem('todos', JSON.stringify(this.todos))
      },
      deep: true
      
    }
  },
  created(){
    this.set()
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.check {
  cursor: pointer;
  
}
.add {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  width: 35%;
  /* margin: 10px; */
  margin-top: 50px;
  margin: 0 5em;
}
.h1 {
  margin-left: 4em;
  text-align: center;
}
.btn {
  padding: 5px;
  width: 100%;
  font-weight: 600;
  font-size: 19px;
  background-color: #fd995e;
  border: none;
  color: white;
  border-radius: 10px;
}
h1 {
  font-size: 30px;
  text-shadow: 0px 1px 0.5px 1px #1f1e1e;
  font-weight: 600;
  color: #161616;
  margin: 2px;
  font-style: oblique;
}
.btn:hover {
  background-color: #f18c53;
  cursor: pointer;
  padding: 7px;
}
.app-section {
  display: flex;
  align-items: flex-start;
  justify-content: start;
  /* border: 1px solid #e83a64; */
}
.list {
  max-width: 400px;
  width: 400px;
  margin-left: 8em;
  display: flex;
  flex-direction: column;
  position: relative;
}
.each {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  margin: 15px;
  background-color: rgb(223, 243, 194);
  padding: 8px;
  border-radius: 10px;
  max-width: 400px;
  width: 400px;
  height: auto;
  overflow-wrap: break-word;
}
.class{
  color: red;
  font-size: 30px;
}
.n-each{
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  margin: 15px;
  background-color: #f5dbcc;
  padding: 8px;
  border-radius: 10px;
  max-width: 400px;
  width: 400px;
  height: auto;
  overflow-wrap: break-word;
}
.cancel {
  color: red;
  font-weight: 600;
  /* margin: 6px; */
  margin: 1px 0 0 20em;
  font-size: 18px;
  cursor: pointer;
}
h3 {
  margin: 0;
}
H2 {
  margin-bottom: 0;
  color: #f18c53;
  text-transform: capitalize;
}
.ul {
  width: 400px;
  display: flex;
  flex-direction: column;
  /* position: relative; */
  align-items: flex-start;
  justify-content: flex-start;
}
p {
  text-align: center;
  overflow-wrap: break-word;
}
@media screen and (max-width: 500px){
  .app-section{
    flex-direction:column;
    align-items: flex-start;
    justify-content: flex-start;
  }
  .list {
  margin-left: 1em; 
}
.n-each {
  max-width: 500px;
  width: 250px;
  position: ;
}
.each{
  max-width: 500px;
  width: 250px;
}
.cancel {
  margin: 1px 0 0 10em;
}
.h1 {
  margin-left: 1em;
  margin-top: 1em;
  text-align: start;
}
.add {
  align-items: start;
  justify-content: flex-start;
  width: 48%;

}
  
}
</style>

// #f18c53; // #e83a64
