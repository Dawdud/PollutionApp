<template>
  <div class="PollutionList">
    <div v-if="citiesList.length" class="box">
      <div class="media-content">
        <p class="title is-3 is-spaced">list of polluted cities:</p>
        <div class="box" v-for="item in citiesList">
          <div class="media-content">
            <div class="content has-text-centered">
              <p>{{item}}</p>
              <a @click="showModal(item)" class="button is-primary is-outlined">Show more</a>
            </div>
          </div>
        </div>
      </div>
    </div>
    <modal v-show="isModalVisible" @close="closeModal">
      <template v-slot:header>
        <p class="modal-card-title">{{city}}</p>
      </template>
      <template v-slot:body>
        <p>{{cityDescription}}</p>
      </template>
    </modal>
  </div>
</template>

<script>
import axios from "axios";
import modal from "./layout/Modal";
export default {
  name: "CityCart",
  props: ["citiesList"],
  data() {
    return {
      isModalVisible: false,
      modalData: null,
      city: null,
      cityDescription: null
    };
  },

  methods: {
    getDescription(cityName) {
      axios
        .get(
          `https://en.wikipedia.org/w/api.php?origin=*&action=opensearch&search=${cityName}&limit=10&namespace=0`
        )
        .then(resp => {
          this.cityDescription = resp.data[2][0];
        });
    },

    showModal(city) {
      this.city = city;
      this.isModalVisible = true;
      this.getDescription(city);
    },
    closeModal() {
      this.isModalVisible = false;
    }
  },
  components: {
    modal
  }
};
</script>