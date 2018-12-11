<template>
  <div class="todolist">
    <ul>
      <li v-for="(todoItem,index) in list" :key="index">
        <label>
          <input
            type="checkbox"
            :checked="todoItem.status === 'done'"
            @change="changeStatus(todoItem,$event)"
          >
          {{todoItem.name}}
        </label>
      </li>
    </ul>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";
import Todo from "../todo";

@Component({
  props: {
    list: Array
  }
})
export default class todolist extends Vue {
  changeStatus(todoItem: Todo, e: Event) {
    let checked = (<HTMLInputElement>e.target).checked;
    this.$emit("updateTodo", todoItem, { status: checked ? "done" : "todo" });
  }
}
</script>
