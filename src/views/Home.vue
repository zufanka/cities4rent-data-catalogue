<template>
  <div class="home">
    <Catalogue :data = "data"/>
  </div>
</template>

<script>
import datasets from "../../data/db.json";
import Catalogue from "../components/Catalogue.vue"

export default {
  name: 'Home',
  components: { Catalogue },
  data() {
    return {
      data : datasets
    }
  }

}
</script>
