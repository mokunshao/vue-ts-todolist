<template>
  <div class="newTodo">
    <input type="text" v-model="text" @keyup.enter="addTodo">
    <button @click="addTodo">提交</button>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";

@Component
export default class newTodo extends Vue {
  text = "";
  addTodo() {
    this.$emit("addTodo", this.text);
    this.text = "";
  }
}
</script>
