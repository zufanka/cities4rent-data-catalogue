<template lang="html">
  <div class="intro contact highlightLink">
    <p>
      When you are researching a housing topic, it might not be immediately obvious what kind of data you need to get a comprehensive view about the topic you are investigating, where you can find those data, or even whether the data are publicly available at all.
    </p>
    <p>
      Based on the <a href="https://cities4rent.journalismarena.media">Cities for Rent cross-border investigation</a>, the <a href="https://journalismarena.eu/housing">Arena Housing Project</a> has launched this Housing Data Catalogue as a collaborative effort to help investigative journalists and other researchers working on housing.
    </p>
    <p>
      Pick the topic of your interest and a country or a city, and the catalogue will show you which data you require, the links to the datasets that are publicly available datasets, and information about the datasets that are not available and which we are building from scratch at the Housing Project.
    </p>
    <p>
      When you select a topic, the catalogue will also show you a box explaining why those are the data you need to research that topic.
    </p>
    <p>
      You can read more <a href="/About">about the Arena Housing Project</a> and the Housing Data Catalogue and about our <a href="/Methodology">methodology</a>, and if you have any question, comment or criticism, or if you want to contribute data to the catalogue, do <a href="/Contact">get in touch</a>.
    </p>

  </div>
  <div class="filteringOptions">
    <h2 class="browse">Browse our data catalogue</h2>
    <div class="filter">
      <label>Select a topic</label>
      <select v-model="topic">
        <option @click="topic = ''" >--- All ---</option>
        <option v-for="topic in uniqueTopics" :key="topic">
          {{ topic }}
        </option>
      </select>
    </div>
    <div class="filter">
      <label>Show cities from</label>
      <select v-model="country">
        <option @click="country = ''">--- All ---</option>
        <option v-for="country in uniqueCountries" :key="country">
          {{ country }}
        </option>
      </select>
    </div>
    <div class="filter">
      <label class="filter">Select a city</label>
      <select v-model="city">
        <option @click="city = ''">--- All ---</option>
        <option v-for="city in uniqueCities" :key="city">
          {{ city }}
        </option>
      </select>
    </div>
    <div class="filter">
      <label>Select on data availability</label>
      <select v-model="status">
        <option @click="status = ''">--- All ---</option>
        <option v-for="status in uniqueStatuses" :key="status">
          {{ status }}
        </option>
      </select>
    </div>
    <div>
        <button class="reset" @click="resetFilters">Reset all filters</button>
    </div>
  </div>
  <div class="sidebar" v-if="topic">
        <SideBar :topic="topic"/>
    </div>
  <div class="blocksWrapper">
    <div v-for="dataset in computed_items" :key="dataset.id" class="blocks">
        <CatalogueItem :dataset="dataset" />
      </div>
  </div>

</template>

<script>
import CatalogueItem from "../components/CatalogueItem.vue"
import SideBar from "../components/SideBar.vue"
import {showAt, hideAt} from 'vue-breakpoints'

export default {
  props: ['data'],
  components: {CatalogueItem, SideBar, hideAt, showAt},
  data() {
    return {
      topic: '',
      country: '',
      city: '',
      status: '',
    }
  },
  methods: {
    resetFilters() {
      this.topic = ''
      this.country = ''
      this.city = ''
      this.status = ''

    }
  },
  computed: {
    uniqueTopics() {
      let ut = [...new Set(this.data.map(item => item.topic))]
      // console.log(ut)
      return ut.sort()
    },

    uniqueStatuses() {
      let ut = [...new Set(this.data.map(item => item.status))]
      // console.log(ut)

      return ut.sort()
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

      return ut.sort()

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

      return ut.sort()
    },

    computed_items() {
      let filterTopic= this.topic,
          filterCountry= this.country,
          filterCity = this.city,
          filterStatus = this.status

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
          if(filterStatus && filterStatus.length > 0){
            filtered = item.status == filterStatus
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


.blocksWrapper {
  display: inline-block;
  width: 80%;
}

.intro {
  max-width: 80%;
  margin: 0 auto 40px;
  padding: 20px 0 0 0;
}

.browse {
  text-align: center;
  text-transform: uppercase;
  background: #EEF0EB;
  color: #032b44;
  padding: 5px
}

.reset {
  background: #032b44;
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
  width: 25%;
  min-height: 150px;
  padding: 10px;
  border-radius: 10px;
  margin: 10px 10px;
  background: #EEF0EB;
  cursor: pointer;
}

.blocks:hover {
  background: #E8EBE4;
}

</style>
