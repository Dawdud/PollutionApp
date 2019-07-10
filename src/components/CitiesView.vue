<template>
  <div class="is-full">
    <Autocomplete @input="userInput" :items="items" />
    <CityCart :citiesList="citiesList" />
  </div>
</template>
<script>
import Autocomplete from "./Autocomplete";
import CityCart from "./CityCart";
import axios from "axios";
export default {
  name: "app",
  data() {
    return {
      searchedValue: null,
      info: null,
      items: [
        { name: "Poland", code: "PL" },
        { name: "France", code: "FR" },
        { name: "Germany", code: "DE" },
        { name: "Spain", code: "ES" }
      ],
      results: []
    };
  },
  computed: {
    citiesList() {
      const polutedCities = this.results.filter(
        (v, i) => this.results.indexOf(v) === i
      );
      return polutedCities.slice(0, 10);
    }
  },
  methods: {
    userInput(value) {
      const searchedValue = this.items
        .filter(item => item.name.toLowerCase() === value.toLowerCase())
        .map(item => item.code);
      if (searchedValue.length) {
        this.result = [];
        axios
          .get(
            `https://api.openaq.org/v1/measurements?country=${
              searchedValue[0]
            }&sort[]=desc&order_by[]=value&parameter[]=pm25&parameter[]=pm10)`
          )
          .then(resp => {
            console.log(resp);
            this.results = resp.data.results.map(elem => elem.city);
          })
          .catch(error => {
            console.log(error.resp);
          });
      }
    }
  },

  components: {
    Autocomplete,
    CityCart
  }
};
</script>