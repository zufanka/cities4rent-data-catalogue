<template lang="html">
<a :href="dataset.link" target="_blank">
  <div class="dataset" @mouseover="isHovering = true"  @mouseout="isHovering = false" >
    <h2>{{ dataset.name }} in {{ dataset.city }}</h2>
    <div class="status cardLabel">{{dataset.status}}</div>
    <p class="cardDescription">
    <div v-if="!dataset.description">
      Get in touch with us if you like to find out more or help us collect this data.
    </div>
    <div v-else>
      {{ dataset.description}}
    </div></p>
    <div class="labelWrap">
      <div class="topic cardLabel leftLabels">{{dataset.topic}}</div>
      <div v-if="dataset.mreadable" class="mreadable cardLabel rightLabels">machine readable</div>
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
.labelWrap {
  display: flex;
  justify-content: space-between;
}

.dataset h2 {
  font-size: 1.2em;
  text-align: left
}

a {
  text-decoration: none;
  color:inherit;

}

.leftLabels {
  text-align:left;
  max-width: 30%;
  }

.rightLabels {
  text-align:right;
  max-width: 30%;
}

.cardLabel {
  text-align: center;
  padding: 5px;
  border-radius: 10px;
  font-size: 0.8em
}

.topic {
  background: #F49D37;
  color: black;
}

.status {
  background: #3F88C5;
  color: white;
  max-width: 30%
}

.mreadable {
  background: #DC143C;
  color: white;
}

.cardDescription {
  text-align: left;
}

</style>
