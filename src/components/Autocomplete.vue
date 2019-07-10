<template>
  <div class="autocomplete column is-narrow is-three-quaters">
    <input
      class="input is-rounded is-large"
      v-model="search"
      @input="onChange($event)"
      type="text"
      placeholder="choose country"
      @keydown.down="onKeyDown"
      @keydown.up="onKeyUp"
      @keydown.enter="onEnter"
    />
    <ul class="list is-hoverable" v-show="isOpen">
      <li
        class="list-item"
        v-for="(result,i) in results"
        :key="i"
        :class="{'is-active': i=== arrowCounter}"
        @click="setResult(result)"
      >{{result.name}}</li>
    </ul>
  </div>
</template>
<script>
export default {
  name: "autocomplete",
  props: ["items"],
  data() {
    return {
      search: "",
      results: [],
      isOpen: false,
      arrowCounter: -1
    };
  },
  mounted() {
    if (localStorage.search) {
      this.search = localStorage.search;
    }
  },
  watch: {
    search: function(newval) {
      localStorage.search = newval;
      this.$emit("input", this.search);
    }
  },
  methods: {
    onChange(event) {
      this.isOpen = true;

      this.filterResults();
    },
    setResult(result) {
      this.search = result.name;

      this.isOpen = false;
    },
    filterResults() {
      this.results = this.items.filter(item =>
        item.name.toLowerCase().includes(this.search.toLowerCase())
      );
    },
    onKeyDown() {
      if (this.arrowCounter < this.results.length) {
        this.arrowCounter = this.arrowCounter + 1;
      }
    },
    onKeyUp() {
      if (this.arrowCounter > 0) {
        this.arrowCounter = this.arrowCounter - 1;
      }
    },
    onEnter() {
      this.search = this.results[this.arrowCounter].name;

      this.isOpen = false;
      this.arrowCounter = -1;
    }
  }
};
</script>
