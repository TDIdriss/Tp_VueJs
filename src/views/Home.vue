<template>
  <div class="home">
    <p v-if="visible">Maintenant vous me voyez {{message}} </p>
    <button v-on:click="foo()"> OK </button>
    <div v-background>Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua</div>
    <div v-background="green">Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua</div>
<div> <todos-component/></div>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import {Background} from '../directives/Background.directive';
import TodosComponent from '@/components/todos.vue'

@Component({
  components: {
    TodosComponent
  },
  directives:{
    Background
  }
})
export default class Home extends Vue {
  visible = true;
  message = "Andy"
  foo(){
      this.visible = !this.visible;
    }

}
</script>
