<template lang="html">
  <div class="filteringOptions">
    <div class="filter">
      <label>Select topic</label>
      <select v-model="topic">
        <option v-for="topic in uniqueTopics" :key="topic">
          {{ topic }}
        </option>
      </select>
    </div>
    <div class="filter">
      <label>Select country</label>
      <select v-model="country">
        <option v-for="country in uniqueCountries" :key="country">
          {{ country }}
        </option>
      </select>
    </div>
    <div class="filter">
      <label class="filter">Select city</label>
      <select v-model="city">
        <option v-for="city in uniqueCities" :key="city">
          {{ city }}
        </option>
      </select>
    </div>
    <div>
        <button class="reset" @click="resetFilters">Reset Filters</button>
    </div>

  </div>

  <div v-for="dataset in computed_items" :key="dataset.id" class="blocks">
    <CatalogueItem :dataset="dataset" />
  </div>
</template>

<script>
import CatalogueItem from "../components/CatalogueItem.vue"

export default {
  props: ['data'],
  components: {CatalogueItem},
  data() {
    return {
      topic: '',
      country: '',
      city: '',
    }
  },
  methods: {
    resetFilters() {
      this.topic = ''
      this.country = ''
      this.city = ''

    }
  },
  computed: {
    uniqueTopics() {
      let ut = [...new Set(this.data.map(item => item.topic))]
      // console.log(ut)
      return ut
    },

    uniqueCountries() {
      let data = this.data,
          city = this.city

      data = data.filter(function(item){
        let filtered = true

        if(city && city.length > 0){
          filtered = item.city == city
        }
        return filtered
      })

      let ut = [...new Set(data.map(item => item.country))]
      // console.log(ut)
      return ut
    },

    uniqueCities() {
      let data = this.data,
          country = this.country

      data = data.filter(function(item){
        let filtered = true

        if(country && country.length > 0){
          filtered = item.country == country
        }
        return filtered
      })

      //console.log(data)

      let ut = [...new Set(data.map(item => item.city))]
      //console.log(this.data.map(item => item.city))

      return ut
    },

    computed_items() {
      let filterTopic= this.topic,
          filterCountry= this.country,
          filterCity = this.city
      return this.data.filter(function(item){
        let filtered = true

        if(filterTopic && filterTopic.length > 0){
          filtered = item.topic == filterTopic
        }

        if(filtered){
          if(filterCountry && filterCountry.length > 0){
            filtered = item.country == filterCountry
          }
        }

        if(filtered){
          if(filterCity && filterCity.length > 0){
            filtered = item.city == filterCity
          }
        }
        return filtered
      })
    },

    filterByTopic(){
                return this.data.filter(dataset => !dataset.topic.indexOf(this.topic))
            }

  },

}
</script>

<style lang="css">
.reset {
  background: #2c3e50;
  color: white;
  font-weight: bold;
  padding: 10px;
  margin: 10px 0;
  cursor: pointer;
  width: 150px;
  border-style: none;
  border-radius: 10px;
}

.filter {
  vertical-align: top;
  padding: 5px;

}

label {
  margin: 0 5px;
  min-width: 100px
}

option {
  margin: 0 5px;
  min-width: 100px
}

.blocks {
  display: inline-block;
  vertical-align: top;
  width: 30%;
  min-height: 150px;
  padding: 10px;
  border-radius: 10px;
  margin: 10px 10px;
  background: #eee;
  cursor: pointer;
}

.blocks:hover {
  background: #ddd;
}

</style>
