<template>
  <div>
<div class="todo-item" v-bind:class="{'is-complete':todo.completed}">
    <p>
      <input type="checkbox" v-on:change="markComplete" v-bind:checked="todo.completed">
      {{todo.title}}
      <button @click="$emit('del-todo', todo.id)" class="del">x</button>
      </p>
     
  </div>
  </div>
</template>

<script>
  export default {
   name: "TodoItem",
  props: ["todo"],
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
      model:"Coding",

    }),
  methods: {
    markComplete() {
      this.todo.completed = !this.todo.completed;
    }
  }
  }
</script>

<style  scoped>
 .todo-item {
    background: #f4f4f4;
    padding: 30px;
    border-bottom: 1px #ccc dotted;

  }

  .is-complete {
    text-decoration: line-through;
  }
</style>