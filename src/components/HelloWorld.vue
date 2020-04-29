<template>
  <v-container>
    <v-card class="mx-auto"
    max-width="500">
      <v-card-title class="text-center teal">
         Todos List
      </v-card-title>
      <v-card-text>
<v-btn  class="ma-2" outlined color="black" @click="save">Add New</v-btn>
  <v-text-field  
     
      class="new-todo"
      autofocus
      autocomplete="off"
      v-model="defaultItem"
      @keyup.enter="save"
      placeholder="What needs to be done?">
      </v-text-field>
   <AddTodo v-on:add-todo="addTodo" />
 <Todos v-bind:todos="todos" />

      </v-card-text>
     <v-card
    class="mx-auto"
    max-width="500"
  >
    <v-list shaped>
      <v-list-item-group
        v-model="model"
        multiple
      >
        <template v-for="(item, i) in items">
          <v-divider
            v-if="!item"
            :key="`divider-${i}`"
          ></v-divider>

          <v-list-item
            v-else
            :key="`item-${i}`"
            :value="item"
            active-class="cyan--text text--accent-4"
          >
            <template v-slot:default="{ active, toggle }">
              <v-list-item-content>
                <v-list-item-title v-text="item"></v-list-item-title>
              </v-list-item-content>

              <v-list-item-action>
                <v-checkbox
                  :input-value="active"
                  :true-value="item"
                  color="cyan accent-4"
                  @click="toggle"
                ></v-checkbox>
      
             
              </v-list-item-action>
            </template>
          </v-list-item>
        </template>
      </v-list-item-group>
    </v-list>
  </v-card>

    </v-card>
  </v-container>
</template>

<script>
 import axios from 'axios';
 import Todos from '../components/Todos';
import AddTodo from '../components/AddTodo';
  export default {
    name: 'HelloWorld',
     components: {
    Todos,
    AddTodo
  },

    data: () => ({
      todos: [],
      items: [
        'Survey users',
        'Design a prototype',
        'Coding',
        'Reading a book',
        'Go to supermarket',
        'Check emails',
      ],
      defaultItem:"",
      model:"Coding",

    }),
   methods:{
     created() {
    axios.get('https://jsonplaceholder.typicode.com/todos?_limit=5')
      .then(res => this.todos = res.data)
      .catch(err => console.log(err));
  }
   },
   addTodo(newTodo) {
      const { title, completed } = newTodo;

      axios.post('https://jsonplaceholder.typicode.com/todos', {
        title,
        completed
      })
        .then(res => this.todos = [...this.todos, res.data])
        .catch(err => console.log(err));
    },
     save () {
        if (this.items > -1) {
          Object.assign(this.items,this.newTodo)
        } else {
          this.items.push(this.defaultItem)
        }
        this.close()
      },
    // deleteTodo(id) {
    //   axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
    //     .then(res => this.todos = this.todos.filter(todo => todo.id !== id))
    //     .catch(err => console.log(err));
    // },
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
</style>
