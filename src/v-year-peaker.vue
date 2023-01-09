<template>
  <v-date-picker
    ref="yearPicker"
    v-model="selectedYear"
    class="date-picker"
    scrollable
    :color="color"
    :dark="dark"
    :disabled="disabled"
    :elevation="elevation"
    :readonly="readonly"
    :width="width"
    :locale="locale"
    :max="max"
    :min="min"
    @click:year="handleClickYearData"
  >
  </v-date-picker>
</template>

<script>
export default {
  name: 'VYearPeaker',
  props: {
    color: {
      type: String,
      default: undefined
    },
    dark : {
      type: Boolean,
      default: false
    },
    disabled: {
      type: Boolean,
      default: false,
    },
    elevation: {
      type: Number,
      default: undefined
    },
    readonly: {
      type: Boolean,
      default: false,
    },
    width: {
      type: String,
      default: '360',
    },
    locale: {
      type: String,
      default: 'en',
    },
    max: {
      type: String,
      default: (new Date().getUTCFullYear() - 1).toString(),
    },
    min: {
      type: String,
      default: undefined,
    },
    onSelectYear: {
      type: Function,
      default: () => {},
      required: true,
    },
  },
  data() {
    return {
      selectedYear: '',
    };
  },
  mounted() {
    this.$refs.yearPicker.internalActivePicker = 'YEAR';
    this.selectedYear = this.max;
  },
  methods: {
    handleClickYearData() {
      this.selectedYear = this.$refs.yearPicker.inputYear.toString();
      this.onSelectYear(this.selectedYear);
      this.$refs.yearPicker.internalActivePicker = 'YEAR';
    },
  },
};
</script>

<style lang="scss" scoped>
::v-deep .v-date-picker-title__date {
  display: none;
}
::v-deep .v-date-picker-title__year {
  margin: 0;
}
</style>