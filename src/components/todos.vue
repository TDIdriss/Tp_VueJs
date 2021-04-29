<template>
  <div class="todos"> 
      <h1>todosComponent</h1>
      <div> <todo-component-component v-for="item in listtache" :key="item" :tache="item"/> </div>
      <p>Nouvelle tache</p>
      <input type="text" v-model="newtache.intitule">
      <input type="text" v-model="newtache.date">
      <button @click="addtache"> Ajouter</button>
      <button @click="deleteall"> Supprimer les taches</button>
      <button @click="removeEndTask"> Supprimer les taches terminées </button>
      
      <footer v-if="listtache.length!==0"><span>{{nb}}</span></footer>   
  </div>
</template>
<script lang="ts">
  import Vue from 'vue';
  import Component from 'vue-class-component';
  import TodoComponentComponent from '@/components/TODOComponent.vue';


  @Component({
   components: {
    TodoComponentComponent
  },
  })
  export default class TodosComponent extends Vue {
    nb=0;
      listtache=[
        {
          intitule : "Exemple-1",
          etat : "en cours",
          date : "30/04/2021"
        },
        {
          intitule : "Exemple-2",
          etat : "en cours",
          date : "29/05/2021"
        },
        {
          intitule : "Exemple-3",
          etat : "a faire",
          date : "29/05/2021"
        },
        {
          intitule : "Exemple-4",
          etat : "terminé",
          date : "29/05/2021"
        }

      ];

// permet d'ajouter une nouvelle tache 
      newtache={
        intitule:"",
        etat: "a faire",
        date:""
      };

      addtache(){
        this.listtache.push(this.newtache)
        this.comptetache()
        //this.newtache.intitule=""
        //this.newtache.date=""
      }

      deleteall(){
        this.listtache=[]
      }
      removeEndTask(){
         for (const iterator of this.listtache) {
            if (iterator.etat==="terminé") {
              this.listtache.splice(this.listtache.indexOf(iterator),1)  
            }
      }
      }
      comptetache(){
        this.nb=0;
          for (const iterator of this.listtache) {
            if (iterator.etat==="a faire") {
              this.nb++;  
            }
      }
      }
     
     
      created(){
        this.$root.$on("supp", this.removetache)
      }

      removetache(tache){
            console.log(tache);
            console.log(this.listtache.indexOf(tache))
            
            this.listtache.splice(this.listtache.indexOf(tache),1)
            console.log(this.listtache);
            
      }
    mounted (){
      this.comptetache()
      console.log('hello from app');
    }
    
  }

</script>


