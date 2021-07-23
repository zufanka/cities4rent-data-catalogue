<template lang="html">
  <div class="intro">
    <p>
      Jujubes ice cream brownie biscuit jelly beans. Bonbon ice cream caramels pie brownie jelly. Chupa chups I love tootsie roll carrot cake I love I love macaroon. Candy canes pudding macaroon cotton candy tootsie roll candy pie chocolate. Pudding topping halvah powder. Soufflé chocolate gingerbread bonbon lemon drops dragée danish donut. Gingerbread powder wafer macaroon pie cupcake sweet roll.
    </p>
    <p>
      Dessert fruitcake gummi bears. Cake gummi bears dragée. Icing soufflé I love jelly beans soufflé. Chocolate cake I love sweet roll lemon drops tootsie roll lemon drops jelly. Chocolate cake gummi bears sweet liquorice halvah. Oat cake I love I love macaroon chupa chups cotton candy. Donut dragée candy canes apple pie danish gummies macaroon liquorice. Dragée icing dessert. Danish pastry chocolate bar cookie cake chocolate cake dragée. Sugar plum sesame snaps tiramisu fruitcake dessert brownie chupa chups.
    </p>

  </div>
  <div class="filteringOptions">
    <h2 class="browse">Browse our data catalogue</h2>
    <div class="filter">
      <label>Select topic</label>
      <select v-model="topic">
        <option v-for="topic in uniqueTopics" :key="topic">
          {{ topic }}
        </option>
      </select>
    </div>
    <div class="filter">
      <label>Show cities from</label>
      <select v-model="country">
        <option v-for="country in uniqueCountries" :key="country">
          {{ country }}
        </option>
      </select>
    </div>
    <div class="filter">
      <label class="filter">Select a city</label>
      <select v-model="city">
        <option v-for="city in uniqueCities" :key="city">
          {{ city }}
        </option>
      </select>
    </div>
    <div class="filter">
      <label>Select on data availability</label>
      <select v-model="status">
        <option v-for="status in uniqueStatuses" :key="status">
          {{ status }}
        </option>
      </select>
    </div>
    <div>
        <button class="reset" @click="resetFilters">Reset Filters</button>
    </div>

  </div>
    <div>
      <div class="blocksWrapper">
        <div v-for="dataset in computed_items" :key="dataset.id" class="blocks">
          <CatalogueItem :dataset="dataset" />
        </div>
      </div>
      <div class="sidebar" v-if="topic">
        <SideBar :topic="topic"/>
      </div>
  </div>

</template>

<script>
import CatalogueItem from "../components/CatalogueItem.vue"
import SideBar from "../components/SideBar.vue"

export default {
  props: ['data'],
  components: {CatalogueItem, SideBar},
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
      return ut
    },

    uniqueStatuses() {
      let ut = [...new Set(this.data.map(item => item.status))]
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
  width: 78%;
}

.intro {
  max-width: 80%;
  margin: 0 auto 40px;
  padding: 20px 0 0 0;
}

.browse {
  text-align: center;
  text-transform: uppercase;
  background: #032b44;
  color: white;
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
