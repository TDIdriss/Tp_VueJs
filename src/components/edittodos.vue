<template>
  <div class="edittodos">
    <h1>edittodosComponent</h1>

    <form>
      <div class="mb-3">
        <label for="" class="form-label">Intitulé</label>
        <input
          type="text"
          v-model="tache.intitule"
          class="form-control"
          id=""
        />
      </div>
      <button type="submit" class="btn btn-primary" @click="edit">
        Editer
      </button>
    </form>
  </div>
</template>
<script lang="ts">
import { PropType } from "vue";
import { Component, Prop, Vue } from "vue-property-decorator";

interface SampleObject {
  intitule: string;
  etat: string;
  date: string;
}
@Component({})
export default class EdittodosComponent extends Vue {
  @Prop({ type: Object as PropType<SampleObject> })
  private editTache!: SampleObject;
  tache = {};

  edit() {
    this.$root.$emit("edit", this.tache, this.editTache);
  }
  created() {
    this.tache = this.editTache;
  }
  mounted() {
    console.log("hello from app");
  }
}
</script>


