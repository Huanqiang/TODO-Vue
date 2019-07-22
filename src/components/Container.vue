<template>
  <section class="todos-container">
    <InputTodo @insert="insert">
      <SelectedAll
        :isAllCompleted="completedAll"
        @toggle-all="toggleAll"
      ></SelectedAll>
    </InputTodo>
    <TodoItem
      v-for="todo in showedTodos"
      :key="todo.id"
      :todo="todo"
      @toggle="toggle"
      @edited="edited"
      @deleted="deleted"
    ></TodoItem>
    <TodoInfos @show="show">
      <template v-slot:count>
        <div>{{ todos.length }} items left</div>
      </template>
      <template v-slot:clear>
        <div @click="clear">Clear completed</div>
      </template>
    </TodoInfos>
  </section>
</template>
<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import Todo from '@/model/todo';
import SelectedAll from '@/components/SelectedAll.vue';
import InputTodo from '@/components/InputTodo.vue';
import TodoItem from '@/components/TodoItem.vue';
import TodoInfos from '@/components/TodoInfo.vue';
@Component({
  components: { SelectedAll, TodoItem, InputTodo, TodoInfos }
})
export default class Container extends Vue {
  private todos: Array<Todo> = [
    {
      id: 1,
      label: '123',
      isCompleted: false
    },
    {
      id: 2,
      label: '456',
      isCompleted: true
    }
  ];
  private completedAll: boolean = false;
  private type = 'all';

  // computed
  get showedTodos() {
    if (this.type === 'all') {
      return this.todos;
    } else if (this.type === 'active') {
      return this.todos.filter(todo => !todo.isCompleted);
    } else {
      return this.todos.filter(todo => todo.isCompleted);
    }
  }

  private insert(label: string): void {
    const id =
      this.todos.length === 0 ? 0 : this.todos[this.todos.length - 1].id + 1;
    this.todos.push({
      id,
      label,
      isCompleted: false
    });
  }
  private toggleAll(value: boolean): void {
    this.completedAll = value;
    this.todos = this.todos.map(todo => ({
      ...todo,
      isCompleted: value
    }));
  }

  private toggle(id: number): void {
    this.todos = this.todos.map(todo => {
      return todo.id === id
        ? { ...todo, isCompleted: !todo.isCompleted }
        : todo;
    });
    this.completedAll =
      this.todos.filter(todo => !!todo.isCompleted).length ===
      this.todos.length;
  }
  private edited(id: number, label: string): void {
    console.log('fdsfs', label);
    this.todos = this.todos.map(todo => {
      return todo.id === id ? { ...todo, label } : todo;
    });
  }
  private deleted(id: number): void {
    this.todos = this.todos.filter(todo => todo.id !== id);
  }

  private show(type: string): void {
    this.type = type;
  }
  private clear(): void {
    this.todos = [];
  }
}
</script>

<style lang="scss">
$shadow: rgb(206, 206, 206);
.todos-container {
  box-shadow: 0px 0px 9px 0px $shadow, 0 30px 50px 0px rgba(0, 0, 0, 0.1);
}
</style>
