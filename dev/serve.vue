<script>
import Vue from 'vue';
import VYearPeaker from '@/v-year-peaker.vue';

export default Vue.extend({
  name: 'ServeDev',
  components: {
    VYearPeaker
  },
  data: () => ({
    selectedYear:(new Date().getUTCFullYear() - 1).toString(),
  }),
  methods: {
    setSelectedYear(input) {
      this.selectedYear = input;
    },
  }
});
</script>

<template>
  <div id="app">
    <v-year-peaker :on-select-year="setSelectedYear"/>
  </div>
</template>
