<template>
  <div>
    {{ msg }}
    <form>
      <button @click="addTodo">ADD TASK</button>
      <button @click="removeTodo">DELETE FINISHED TASKS</button>
      <p>input: <input type="text" v-model="newTodo"></p>
      <p>task: {{ newTodo }}</p>
    </form>
    <div class="task-list">
      <label class="task-list__item" v-for="todo in todos" v-bind:class="{ 'task-list__item--checked': todo.done }">
        <input type="checkbox" v-model="todo.done">
        <input type="checkbox" v-model="todo.editing">
        <input type="text" v-if="todo.editing" v-model="todo.text" @keyup.enter="todo.editing = !todo.editing">
        <span v-else>{{ todo.text }}</span>
      </label>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'hello',
    data () {
      return {
        msg: 'Welcome to your Vue.js App',
        todos: [
          {
            text: 'vue-router',
            done: false,
            editing: false,
          },
          {
            text: 'vuex',
            done: false,
            editing: false,
          },
          {
            text: 'vue-loader',
            done: false,
            editing: false,
          },
          {
            text: 'awesome-vue',
            done: true,
            editing: false,
          },
        ],
        newTodo: '',
      }
    },
    methods: {
      addTodo (_e) {
        let text = this.newTodo && this.newTodo.trim()
        if (!text) return
        this.todos.push({
          text,
          done: false,
          editing: false,
        })
        this.newTodo = ''
      },
      removeTodo (_e) {
//        どっちがいいのかよくわからない
//        for (let i = this.todos.length - 1; i >= 0; i--) {
//          if (this.todos[i].done) this.todos.splice(i, 1)
//        }
        this.todos = this.todos.filter(t => !t.done)
      },
    },
  }
</script>


<style lang="scss" scoped>
  @mixin flex-vender() {
    display: flex;
    display: -webkit-flex;
    display: -moz-flex;
    display: -ms-flex;
    display: -o-flex;
  }

  .task-list {
    @include flex-vender;
    flex-direction: column;
    align-items: center;
    &__item {
      width: 270px;
      text-align: left;
      $element: #{&};
      &--checked {
        @extend #{$element};
        color: #85a6c6;
      }
    }
  }
</style>
