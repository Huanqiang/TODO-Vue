<template>
  <div class="input-todo">
    <slot></slot>
    <input
      class="input"
      placeholder="What needs to be done?"
      v-model="label"
      @keyup.enter="inputEnd"
    />
  </div>
</template>
<script lang="ts">
import Vue from 'vue';
export default Vue.extend({
  data() {
    return {
      label: ''
    };
  },
  methods: {
    inputEnd: function() {
      if (this.label === '') {
        return;
      }
      this.$emit('insert', this.label);
      this.label = '';
    }
  }
});
</script>
<style lang="scss">
.input-todo {
  position: relative;
  padding: 8px 16px;
  border-bottom: 1px rgb(226, 226, 226) solid;
}

.input-todo .input {
  margin-left: 24px;
  font: 100 24px system-ui;
  width: 90%;
  outline: none;
  border: none;
  -webkit-font-smoothing: antialiased;
}
</style>
