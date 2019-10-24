<template lang="html">
  <div>
    <h1>Countries</h1>
    <country-filter-form :countries="countries" />
    <country-detail />
  </div>
</template>
<!-- display CountryFilterForm with contents of countries array and
display CountryDetail -->

<script>
import CountryFilterForm from './components/CountryFilterForm.vue'
import CountryDetail from './components/CountryDetail.vue'
//import the component files
export default {
  data(){
    return {
      countries: [],
    }
    //make countries array accessible for CountryFilterForm
    //and countryDetail
  },
  components: {
    "country-filter-form": CountryFilterForm,
    "country-detail": CountryDetail
    //setup components using correct casing
  },
  mounted(){
    fetch('https://restcountries.eu/rest/v2/all')
    .then(res => res.json())
    .then(countries => this.countries = countries)
  }
  //fetch data from app on page load and put it into countries array
}
</script>

<style lang="css" scoped>
h1 {
  text-align: center;
  color: #333;
}
</style>
