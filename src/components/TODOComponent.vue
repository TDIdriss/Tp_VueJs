<template>
  <div class="todo-component"> 
      <h1>todo-componentComponent</h1>

      <h1 @click="update">intitulé : {{tache.intitule}}</h1>
      <h1>etat : {{tache.etat}}</h1>
      <h1>date : {{tache.date}}</h1>
      <button @click="deletetache">Suppprimer</button>
      <div v-if="openmodal"> <edittodos-component :editTache="tache"/> </div>
      
  </div>
</template>
<script lang="ts">
  
import { PropType } from 'vue';
  import { Component, Prop, Vue } from 'vue-property-decorator';
  import EdittodosComponent from "@/components/edittodos.vue"

interface SampleObject{
   intitule : string,
   etat : string,
   date : string
 } 
  @Component({
      components : {
        EdittodosComponent
      }
  })
  export default class TodoComponentComponent extends Vue {
    @Prop({type:Object as PropType<SampleObject> }) private tache!:SampleObject;
     
     openmodal=false

     deletetache(){
      this.$root.$emit("supp", this.tache) 
     }
     update(){
        this.openmodal=true
        console.log("ici");
        console.log(this.openmodal);
        
        
     }
    mounted (){
      console.log('hello from app');
    }
    
  }

</script>


