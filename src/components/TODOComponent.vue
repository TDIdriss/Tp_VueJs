<template>
  <div class="todo-component"> 
      <h1>todo-componentComponent</h1>

      <h1>intitulé : {{tache.intitule}}</h1>
      <h1>etat : {{tache.etat}}</h1>
      <h1>date : {{tache.date}}</h1>
      <button @click="deletetache">Suppprimer</button>
      
  </div>
</template>
<script lang="ts">
  
import { PropType } from 'vue';
  import { Component, Prop, Vue } from 'vue-property-decorator';




interface SampleObject{
   intitule : string,
   etat : string,
   date : string
 } 
  @Component({})
  export default class TodoComponentComponent extends Vue {
    @Prop({type:Object as PropType<SampleObject> }) private tache!:SampleObject;
     
     deletetache(){
      this.$root.$emit("supp", this.tache) 
     }
    mounted (){
      console.log('hello from app');
    }
    
  }

</script>


