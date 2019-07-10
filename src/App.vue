<template>
  <div id="app">
    <Header></Header>
    <div class="columns is-full is-centered is-vcentered">
      <CitiesView />
    </div>
  </div>
</template>

<script>
import CitiesView from "./components/CitiesView";
import Header from "./components/layout/Header";

export default {
  name: "app",
  data() {
    return {
      searchedValue: null
    };
  },

  components: {
    CitiesView,
    Header
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
}

.columns.is-vcentered {
  -webkit-box-align: center;
  -ms-flex-align: center;
  align-items: center;
}
</style>
