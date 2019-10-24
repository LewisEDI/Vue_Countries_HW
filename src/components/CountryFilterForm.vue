<template lang="html">
  <form v-on:submit.prevent>
    <input type="text" v-model="search" placeholder="search for country..." v-on:keyup="searchForCountry">
    <!-- searchbox assigns input to search string and calls searchForCountry function when enter is pressed -->
    <select v-on:change="handleSelect" v-model="selectedCountry">
      <option disabled value="">Select a country...</option>
      <option v-for="country in countries" :value="country">{{country.name}}</option>
    </select>
    <!-- drop box list assigns country selected to SelectedCountry and calls handleSelect function when country is selected -->

  </form>
</template>

<script>
import { eventBus } from '../main.js'

export default {
  name: "country-filter-form",
  data(){
    return {
      "search": "",
      "selectedCountry": {},
    }
    //exports search and SelectedCountry
  },
  props: ["countries"],
  // use the imported countries property
  methods: {
    searchForCountry(){
      let foundCountry = this.countries.find((country) => {
        return country.name.toLowerCase().indexOf(this.search.toLowerCase()) > -1
      })
      //FoundCountry is set to the country in the array that matches the value entred
      //in the search box. callback function is called that sets country name to lower case, not sure what
      // is happening with the index?
      this.selectedCountry = foundCountry
      //the country found is set to be the SeletedCountry

      eventBus.$emit('country-selected', this.selectedCountry)
      //broadcast that the country has been selected (via the search)
    },
    handleSelect(){
      this.search = ""
      eventBus.$emit('country-selected', this.selectedCountry)
      //this.seatch set to null as it has not been used.
      //broadcast that the country has been seected via the drop down menu.

    }
  }
}
</script>

<style lang="css" scoped>
form{
  text-align: center;
  margin: 40px 0;
}

select, input[type="text"]{
  font-size: 18px;
}

select {
  margin-left: 20px;
}
</style>
