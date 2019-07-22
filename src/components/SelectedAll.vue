<template>
  <div>
    <input
      class="check"
      type="checkbox"
      @click="toggledAll"
      :checked="isAllCompleted"
    >
    <label>❯</label>
  </div>
</template>
<script lang="ts">
import Vue from 'vue';
export default Vue.extend({
  props: {
    isAllCompleted: Boolean
  },
  data() {
    return {};
  },
  methods: {
    toggledAll: function() {
      this.$emit('toggle-all', !this.isAllCompleted);
    }
  }
});
</script>
<style lang="scss">
.check {
  opacity: 0;
  position: absolute;
  left: 8px;
  top: 8px;
  width: 22px;
  height: 22px;
  cursor: pointer;
  outline: 1px brown solid;
}

.check:checked + label {
  color: #4d4d4d;
}

.check + label {
  position: absolute;
  display: inline-block;
  transform: rotate(90deg);
  font-size: 22px;
  color: #b4b1b1;
  cursor: pointer;
  z-index: -1;
}
</style>
