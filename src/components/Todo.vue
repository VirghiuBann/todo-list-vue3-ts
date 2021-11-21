<template>
  <div>
    <h1>Todo List App</h1>
    <InputBase @addText="addText" />
    <div class="todo__list-container">
      <ul>
        <li v-for="item in todos" :key="item.id">
          <div>
            <strong>{{ item.id }}</strong>
            <span>{{ item.text }} </span>
            <span>{{ item.createdAt }}</span>
            <button @click="destroy(item)">X</button>
          </div>
        </li>
      </ul>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import InputBase from './InputBase.vue';

interface Todo {
  id: number;
  text: string;
  createdAt: string;
}

type TodoList = Todo[];

export default defineComponent({
  name: 'Todo',
  components: {
    InputBase,
  },
  data() {
    return {
      todos: [
        {
          id: 1,
          text: 'fisrt text',
          createdAt: new Date().toISOString(),
        },
      ] as TodoList,
    };
  },

  methods: {
    addText(text: string): void {
      const item: Todo = {
        id: this.todos.length + 1,
        text: text,
        createdAt: new Date().toISOString(),
      };

      this.todos.push(item);
    },

    destroy(item: Todo): void {
      const items: Todo[] = this.todos.filter((todo) => todo.id !== item.id);
      this.todos = items;
    },
  },
});
</script>

<style scoped>
li {
  list-style: none;
}
</style>
