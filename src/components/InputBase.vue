<template>
  <div>
    <input type="text" v-model="text" @keyup.enter="onSubmit" />
    <button @click="onSubmit">Add</button>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'Input',
  emits: {
    addText(text: string) {
      // perform runtime validation
      if (text == '' || text.trim() == '') {
        throw new Error('invalid data.');
      }
      return text.length > 0;
    },
  },
  data() {
    return {
      text: '' as string,
    };
  },

  methods: {
    onSubmit() {
      if (this.text == '' || this.text.trim() == '') return;

      this.$emit('addText', this.text);
      this.text = '';
    },
  },
});
</script>

<style scoped></style>
