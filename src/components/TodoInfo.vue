<template>
  <div class="todo-infos">
    <slot name="count"></slot>
    <ul class="todo-state">
      <li :class="{selected: allClass}"><a @click="showAll">All</a></li>
      <li :class="{selected: activeClass}"><a @click="showActive">Active</a></li>
      <li :class="{selected: completedClass}"><a @click="showCompleted">Completed</a></li>
    </ul>
    <slot name="clear"></slot>
  </div>
</template>
<script lang="ts">
import Vue from 'vue';
export default Vue.extend({
  data() {
    return {
      allClass: true,
      activeClass: false,
      completedClass: false
    };
  },
  methods: {
    showAll() {
      this.setShowType('all');
    },
    showActive() {
      this.setShowType('active');
    },
    showCompleted() {
      this.setShowType('completed');
    },
    setShowType(type: string) {
      this.$emit('show', type);
      this.allClass = false;
      this.activeClass = false;
      this.completedClass = false;
      if (type === 'all') {
        this.allClass = true;
      } else if (type === 'active') {
        this.activeClass = true;
      } else {
        this.completedClass = true;
      }
    }
  }
});
</script>
<style lang="scss">
.todo-infos {
  display: flex;
  justify-content: space-between;
  padding: 8px 8px;
  margin-bottom: 32px;
  color: #777;
  font-size: 14px;
  font-weight: 300;
  box-shadow: 0 1px 1px rgba(0, 0, 0, 0.2), 0px 7px 0px -2px rgb(255, 255, 255),
    0px 8px 1px -2px rgba(0, 0, 0, 0.15), 0px 14px 0px -4px rgb(255, 255, 255),
    0px 15px 1px -4px rgba(0, 0, 0, 0.15);
}

.todo-infos .todo-state {
  display: flex;
  justify-content: space-between;
  margin: 0px;
  /* height: 22px; */
}

.todo-infos .todo-state li {
  display: inline;
  padding: 1px 4px;
  margin: 0 4px 0 0px;
  cursor: pointer;
  list-style: none;

  border: 1px transparent solid;
  border-radius: 3px;
}

.todo-infos .todo-state li.selected {
  border: 1px sandybrown solid;
}

.todo-infos .todo-state li.selected:hover {
  border: 1px sandybrown solid;
}

.todo-infos .todo-state li:hover {
  border: 1px rgba(175, 47, 47, 0.1) solid;
}

.todo-infos div:last-child:hover {
  cursor: pointer;
  text-decoration: underline;
}
</style>
