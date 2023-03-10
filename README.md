# v-year-peaker

### Now You Can Use v-year-peaker w/ vuetify! (1.2.0)

vuetify v-date-peaker is not providing a type: 'year' yet (23.1.10.)

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

Import and Set on components and use It.

```js
<template>
  <v-app>
    <v-year-peaker :on-select-year="setSelectedYear"/>
  </v-app>
</template>

<script>
import VYearPeaker from 'v-year-peaker'

export default {
  name: 'App',
  components: { VYearPeaker },
  data: () => ({
    selectedYear:(new Date().getUTCFullYear() - 1).toString(),
  }),
  methods: {
    setSelectedYear(input) {
      this.selectedYear = input;
    },
  }
};
</script>
```

<img width="300" alt="스크린샷 2023-01-11 오후 8 17 37" src="https://user-images.githubusercontent.com/85068289/211793205-f830bf28-d28d-48d1-a391-fd0ad1a9b498.png">



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

## Next
I hope They Patch soon or I'll try to Contribute on TODO catch update this.
