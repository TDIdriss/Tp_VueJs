<template>
  <div class="todo-component">
    <!--<h1>todo-componentComponent</h1>-->

    <tr>
      <td scope="row" @click="update">{{ tache.intitule }}</td>
      <td scope="row">{{ tache.etat }}</td>
      <td scope="row">{{ tache.date }}</td>
      <td><button @click="deletetache" class="btn btn-primary">Supprimer</button></td>
    </tr>
    <div v-if="openmodal"> <edittodos-component :editTache="tache"/> </div>
  </div>
</template>
<script lang="ts">
import { PropType } from "vue";
import { Component, Prop, Vue } from "vue-property-decorator";
import EdittodosComponent from "@/components/edittodos.vue";

interface SampleObject {
  intitule: string;
  etat: string;
  date: string;
}
@Component({
  components: {
    EdittodosComponent,
  },
})
export default class TodoComponentComponent extends Vue {
  @Prop({ type: Object as PropType<SampleObject> })
  private tache!: SampleObject;

  openmodal = false;

  deletetache() {
    this.$root.$emit("supp", this.tache);
  }
  update() {
    this.openmodal = true;
    console.log("ici");
    console.log(this.openmodal);
  }
  mounted() {
    console.log("hello from app");
  }
}
</script>