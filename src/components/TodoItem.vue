<template>
  <div class="todo-item">
    <input
      class="todo-item-toggle"
      type="checkbox"
      :checked="todo.isCompleted"
      @click="toggled(todo.id)"
    >
    <template>
      <span
        v-if="todo.isCompleted"
        class="todo-item-completed"
        @dblclick="edit"
      >{{ todo.label }}</span>
      <span
        v-else
        ref=uncompletedItem
        @dblclick="edit"
      >{{ todo.label }}</span>
    </template>
    <input
      class="todo-item-edit"
      :class="{hidden: isHidden}"
      v-model="editValue"
      @keyup.enter="editEnd"
    />
    <div
      class="item-delete"
      @click="deleted"
    >
      <span></span>
    </div>
  </div>
</template>
<script lang="ts">
import { Component, Vue, Prop } from 'vue-property-decorator';
import Todo from '@/model/todo';

@Component({})
export default class TodoItem extends Vue {
  @Prop({ default: { id: 0, label: 'qqwe', isCompleted: false } })
  readonly todo!: Todo;
  private isHidden = true;
  private editValue = '';

  public toggled(id: number) {
    this.$emit('toggle', this.todo.id);
  }
  public editEnd(event: any) {
    this.isHidden = true;
    this.$emit('edited', this.todo.id, this.editValue);
    console.log('todo item editEnd', this.editValue);
  }
  public deleted() {
    this.$emit('deleted', this.todo.id);
    console.log('todo item deleted');
  }
  private edit() {
    this.isHidden = false;
    this.editValue = this.todo.label;
    console.log('todo item edit');
  }
}
</script>
<style lang="scss">
.todo-item {
  position: relative;
  /* height: 40px; */
  padding: 12px 8px;
  font-size: 24px;
  font-weight: 200;
  border-bottom: 1px rgb(226, 226, 226) solid;
}

.todo-item-completed {
  text-decoration: line-through;
  color: #d9d9d9;
}

.todo-item-toggle {
  position: absolute;
  top: 0;
  left: 0;
  width: 40px;
  height: 40px;
  cursor: pointer;
  outline: none;
  appearance: none;
  -webkit-appearance: none;
}

.todo-item-toggle + span {
  display: inline-block;
  margin-left: 0px;
  padding-left: 48px;
  font-weight: inherit;
}

.todo-item-toggle + span {
  content: '';
  background-image: url(data:image/svg+xml;utf8,%3Csvg%20xmlns%3D%22http%3A//www.w3.org/2000/svg%22%20width%3D%2240%22%20height%3D%2240%22%20viewBox%3D%22-10%20-18%20100%20135%22%3E%3Ccircle%20cx%3D%2250%22%20cy%3D%2250%22%20r%3D%2250%22%20fill%3D%22none%22%20stroke%3D%22%23ededed%22%20stroke-width%3D%223%22/%3E%3C/svg%3E);
  background-repeat: no-repeat;
  background-position: center left;
}

.todo-item-toggle:checked + span {
  content: '';
  background-image: url(data:image/svg+xml;utf8,%3Csvg%20xmlns%3D%22http%3A//www.w3.org/2000/svg%22%20width%3D%2240%22%20height%3D%2240%22%20viewBox%3D%22-10%20-18%20100%20135%22%3E%3Ccircle%20cx%3D%2250%22%20cy%3D%2250%22%20r%3D%2250%22%20fill%3D%22none%22%20stroke%3D%22%23bddad5%22%20stroke-width%3D%223%22/%3E%3Cpath%20fill%3D%22%235dc2af%22%20d%3D%22M72%2025L42%2071%2027%2056l-4%204%2020%2020%2034-52z%22/%3E%3C/svg%3E);
  background-repeat: no-repeat;
  background-position: center left;
}

.todo-item-edit {
  position: absolute;
  top: 8px;
  left: 52px;
  height: 36px;
  font-size: 24px;
  font-weight: 200;
}

.item-delete {
  position: absolute;
  right: 12px;
  top: 8px;
  width: 40px;
  height: 40px;
  cursor: pointer;
}

.item-delete:hover span {
  opacity: 1;
}

.item-delete span {
  opacity: 0;
  position: absolute;
  right: 12px;
  top: 20px;
  width: 12px;
  height: 1px;
  background-color: #cc9a9a;
  transform: rotate(45deg);
}

.item-delete span::before {
  content: '';
  position: absolute;
  right: 0px;
  top: 0px;
  width: 12px;
  height: 1px;
  background-color: #cc9a9a;
  transform: rotate(-90deg);
}

.hidden {
  display: none;
}
</style>
