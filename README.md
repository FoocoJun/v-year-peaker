# v-year-peaker

vuetify v-date-peaker do not provide type: 'year' (23.1.10.)

You can use this year-peaker to Resolve vuetify's v-date-peaker TODO.

```js
 type: {
      type: String,
      default: 'date',
      validator: (type: any) => ['date', 'month'].includes(type), // TODO: year
    } as PropValidator<DatePickerType>,
```


## Get-Started

```
npm i v-year-peaker
```

## How-It-Works

we provide most props of v-date-peaker , vuetify.

```js
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
```

### when this component mounted
```js
mounted() {
  this.$refs.yearPicker.internalActivePicker = 'YEAR';
  this.selectedYear = this.max;
},
```
the internalActivePicker become 'YEAR'

and it trigger to rerender v-date-peaker w/ activePicker 'YEAR'

### after selecting year
Event `@click:year` w/ `handleClickYearData`

```js
handleClickYearData() {
  this.selectedYear = this.$refs.yearPicker.inputYear.toString();
  this.onSelectYear(this.selectedYear);
  this.$refs.yearPicker.internalActivePicker = 'YEAR';
},
```
default event changes `internalActivePicker` to 'MONTH'

but this handler holds `internalActivePicker` as 'YEAR'

## Required-And-Sample
make sure set setter methods(to get selectedYear) to onSelectYear property

```js
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
```
