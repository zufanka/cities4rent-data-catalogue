<template lang="html">
    <h2>{{ activeTopic[0].headline }}</h2>
    <p>{{ activeTopic[0].description }}</p>
</template>

<script>
import topicDescriptions from "../../data/topic_descriptions.json";

export default {
  name: 'SideBar',
  props: ['topic'],
  data() {
    return {
      data : topicDescriptions,
    }
  },
  methods : {
    showdata() {
      console.log(this.data)
      console.log(this.topic)
    }
  },
  computed: {
    activeTopic() {
      let filterTopic = this.topic

      return this.data.filter(function(item){
        let filtered = true

        if(filterTopic && filterTopic.length > 0){
          filtered = item.topic == filterTopic
        }
        return filtered
      })
    }
  }
}
</script>

<style lang="css">
.sidebar {
  display: inline-block;
  width:85%;
  vertical-align: top;
  border: 1px solid black;
  margin: 0 15px 0 0;
  padding: 0 10px;
  border-radius: 4px;
  text-align: left;
  font-size: 0.9em
}
</style>
