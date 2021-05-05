<template>
  <div class="todos">
    <nav class="navbar navbar-expand-lg navbar-light bg-light">
      <div class="container-fluid">
        <a class="navbar-brand" href="">TP VUEJS</a>
        <button
          class="navbar-toggler"
          type="button"
          data-bs-toggle="collapse"
          data-bs-target="#navbarSupportedContent"
          aria-controls="navbarSupportedContent"
          aria-expanded="false"
          aria-label="Toggle navigation"
        >
          <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse" id="navbarSupportedContent">
          <ul class="navbar-nav me-auto mb-2 mb-lg-0">
            <li class="nav-item">
              <a class="nav-link active" aria-current="page" href="/">Todo</a>
            </li>
          </ul>
        </div>
      </div>
    </nav>

    <div class="row">
      <div class="col-12">
        <div class="card">
          <div class="card-header">
            <button class="btn btn-danger" @click="deleteall">
              Supprimer les taches
            </button>
            <button class="btn btn-primary" @click="removeEndTask">
              Supprimer les taches terminées
            </button>
          </div>
          <div class="card-body">
            <h5 class="card-title">Nouvelle tâche</h5>
            <form>
              <div class="mb-3">
                <label for="" class="form-label">Intitulé</label>
                <input
                  type="text"
                  v-model="newtache.intitule"
                  class="form-control"
                  id=""
                />
              </div>
              <div class="mb-3">
                <label for="" class="form-label">Date</label>
                <input
                  type="text"
                  v-model="newtache.date"
                  class="form-control"
                  id=""
                />
              </div>
              <button type="submit" class="btn btn-primary" @click="addtache">
                Ajouter
              </button>
            </form>
            <hr />
            <h5 class="card-title">Tâches</h5>
            <table class="table">
              <thead>
                <tr>
                  <th scope="col">Titre</th>
                  <th scope="col">Etat</th>
                  <th scope="col">Date</th>
                  <th scope="col"></th>
                </tr>
              </thead>
              <tbody>
                <todo-component-component
                  v-for="item in listtache"
                  :key="item"
                  :tache="item"
                />
              </tbody>
            </table>
            <hr>
            <div class="card-footer" v-if="listtache.length !== 0">
              Nombre de tâche à faire
              <span class="badge bg-success">{{nb}}</span>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script lang="ts">
import Vue from "vue";
import Component from "vue-class-component";
import TodoComponentComponent from "@/components/TODOComponent.vue";

@Component({
  components: {
    TodoComponentComponent,
  },
})
export default class TodosComponent extends Vue {
  nb = 0;
  listtache = [
    {
      intitule: "Exemple-1",
      etat: "en cours",
      date: "30/04/2021",
    },
    {
      intitule: "Exemple-2",
      etat: "en cours",
      date: "29/05/2021",
    },
    {
      intitule: "Exemple-3",
      etat: "a faire",
      date: "29/05/2021",
    },
    {
      intitule: "Exemple-4",
      etat: "terminé",
      date: "29/05/2021",
    },
  ];

  // permet d'ajouter une nouvelle tache
  newtache = {
    intitule: "",
    etat: "a faire",
    date: "",
  };

  addtache() {
    this.listtache.push(this.newtache);
    this.comptetache();
    //this.newtache.intitule=""
    //this.newtache.date=""
  }

  deleteall() {
    this.listtache = [];
  }
  removeEndTask() {
    for (const iterator of this.listtache) {
      if (iterator.etat === "terminé") {
        this.listtache.splice(this.listtache.indexOf(iterator), 1);
      }
    }
  }
  comptetache() {
    this.nb = 0;
    for (const iterator of this.listtache) {
      if (iterator.etat === "a faire") {
        this.nb++;
      }
    }
  }

  created() {
    this.$root.$on("supp", this.removetache);
    this.$root.$on("edit", this.edittache);
  }

  edittache(newtache, tache) {
    console.log(newtache);
    console.log(tache);
    console.log(this.listtache.indexOf(tache));

    this.listtache.splice(this.listtache.indexOf(tache), 1, newtache);
    console.log(this.listtache);
  }

  removetache(tache) {
    console.log(tache);
    console.log(this.listtache.indexOf(tache));

    this.listtache.splice(this.listtache.indexOf(tache), 1);
    console.log(this.listtache);
  }
  mounted() {
    this.comptetache();
    console.log("hello from app");
  }
}
</script>

<style scoped>
.card {
  margin-left: 5%;
  margin-right: 5%;
}
</style>
