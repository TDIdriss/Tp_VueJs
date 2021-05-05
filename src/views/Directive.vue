<template>
  <div class="directive">
    <p v-if="visible">Maintenant vous me voyez {{message}} </p>
    <button v-on:click="foo()"> OK </button>
    <div v-background>Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua</div>
    <div v-background="green">Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua</div>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import {Background} from '../directives/Background.directive';

@Component({
  components: {

  },
  directives:{
    Background
  }
})
export default class Directive extends Vue {
  visible = true;
  message = "Bonjour!"
  foo(){
      this.visible = !this.visible;
    }

}
</script>