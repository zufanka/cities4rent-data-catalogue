<template lang="html">
<a :href="dataset.link">
  <div class="dataset" @mouseover="isHovering = true"  @mouseout="isHovering = false" >
    <h2>{{ dataset.name }} in {{ dataset.city }}</h2>
    <p> {{ dataset.status}}</p>
    <div class="topic">
      {{ dataset.topic}}
    </div>
    <div v-if="dataset.mreadable" class="mreadable">
      machine readable
    </div>
  </div>
</a>
</template>

<script>
export default {
    props: ['dataset'],
    data() {
      return{
        isHovering: false,
      }
    }
}
</script>

<style lang="css">

h2 {
  font-size: 1.3em;
  text-align: left
}

a {
  text-decoration: none;
  color:inherit;
}

.topic {
  text-align: center;
  background: #913644;
  color: white;
  max-width: 30%;
  padding: 5px;
  float:left;
  border-radius: 10px;
}

.mreadable {
  text-align: center;
  background: #c6b52f;
  color: white;
  max-width: 30%;
  padding: 5px;
  float:right;
  border-radius: 10px;
}

</style>
