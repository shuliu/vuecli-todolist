<template>
  <div id="selector">
    <Selector v-model="cityIndex" :list="getCity"></Selector>
    <Selector v-model="townIndex" :list="getTown"></Selector>
    <span class="zip">{{getZip}}</span>
  </div>
</template>

<script>
import axios from 'axios';
// import _ from 'lodash';
import { API } from '../environment.js';
import Selector from "@/components/Selector.vue";

export default {
  components: {
    Selector
  },
  data() {
    return {
      cities: [],
      cityIndex: 0,
      townIndex: 0,
    }
  },
  created() {
    // this.cities;
    const url = `${API}/cities`
    axios
      .get(url)
      .then((response) => {
        if(response.status === 200) {
          this.cities = response.data;
        }
      })
      .catch(e => console.log(e));
  },
  mathods: {
  },
  computed: {
    getCity() {
      return this.cities || [];
    },
    getTown: function() {
      return this.cities.length > 0 ? this.cities[this.cityIndex].areas : [];
    },
    getZip: function() {
      const areas = this.getTown || [];
      if(areas.length <= 0) {
        return '';
      }
      return areas[this.townIndex].zip || '';
    },
  },
  watch: {
    cityIndex() {
      this.townIndex = 0;
    }
  },
}
</script>


<style>

</style>
