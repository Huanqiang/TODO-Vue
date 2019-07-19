<template>
  <div class="input-todo">
    <input class="check" type="checkbox" @click="toggledAll" :checked="isAllCompleted"> 
    <label>❯</label>
  <input class="input" placeholder="What needs to be done?" v-model="label" @keyup.enter="inputEnd"/>
</div>
</template>
<script lang="ts">
import Vue from 'vue';
export default Vue.extend({
  props: {
    isAllCompleted: Boolean
  },
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
    },
    toggledAll: function() {
      this.$emit('toggle-all', !this.isAllCompleted);
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

.input-todo .check {
  opacity: 0;
  position: absolute;
  left: 8px;
  top: 8px;
  width: 22px;
  height: 22px;
  cursor: pointer;
  outline: 1px brown solid;
}

.input-todo .check:checked + label {
  color: #4d4d4d;
}

.input-todo label {
  position: absolute;
  display: inline-block;
  transform: rotate(90deg);
  font-size: 22px;
  color: #b4b1b1;
  cursor: pointer;
  z-index: -1;
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
