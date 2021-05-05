<template>
  <div class="home">
    <div><todos-component /></div>
    
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import { Background } from "../directives/Background.directive";
import TodosComponent from "@/components/todos.vue";

@Component({
  components: {
    TodosComponent,
  },
  directives: {
    Background,
  },
})
export default class Home extends Vue {
  visible = true;
  message = "Andy";
  foo() {
    this.visible = !this.visible;
  }
}
</script>
