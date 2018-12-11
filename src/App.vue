<template>
  <div id="app">
    <newTodo @addTodo="addTodo"/>
    <todoList :list="list" @updateTodo="updateTodo"/>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import Todo from "./todo";
import newTodo from "./components/newTodo.vue";
import todoList from "./components/todoList.vue";


@Component({
  components: {
    newTodo,
    todoList
  },
  watch: {
    list(newValue:Array<Todo>) {
      let string = JSON.stringify(newValue);
      localStorage.setItem("data", string);
    }
  }
})
export default class App extends Vue {
  list: Array<Todo> = localStorage.getItem("data")?JSON.parse(<string>localStorage.getItem("data")):[];
  addTodo(name: string) {
    let todo: Todo = { name: name, status: "todo" };
    this.list.unshift(todo);
  }
  updateTodo(todo: Todo, part: Partial<Todo>) {
    let index: number = this.list.indexOf(todo);
    let newTodo: Todo = Object.assign({}, todo, part);
    this.list.splice(index, 1, newTodo);
  }
}
</script>

<style lang="scss">
li {
  list-style: none;
}
</style>
