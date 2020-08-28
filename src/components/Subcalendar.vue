<template>
  <v-row>
    <v-col cols="4" v-for="(i, index) in months" :key="index">
      <Month :months="i" />
    </v-col>
  </v-row>
</template>

<script>
import Month from './Month'
export default {
  data() {
    return {
      months: [],
      dayim: [0, 31, 59, 90, 120, 151, 181, 212, 243, 273, 304, 334, 365]
    }
  },
  components: {
    Month
  },
  props: {
    index: Number
  },
  async mounted() {
    this.render()
  },
  watch: {
    index() {
      console.log(this.index)
      this.render()
    }
  },
  methods: {
    render() {
      this.months = []
      for (let i = 1; i <= 12; i++) {
        if (i == 2 && this.index > 7) {
          this.months.push({
            month: i,
            start: (this.index + this.dayim[i - 1] - 1) % 7,
            end: this.dayim[i] - this.dayim[i - 1] + 1
          })
        } else if (i > 2 && this.index > 7) {
          this.months.push({
            month: i,
            start: (this.index + this.dayim[i - 1]) % 7,
            end: this.dayim[i] - this.dayim[i - 1]
          })
        } else {
          this.months.push({
            month: i,
            start: (this.index + this.dayim[i - 1] - 1) % 7,
            end: this.dayim[i] - this.dayim[i - 1]
          })
        }
      }
    }
  }
}
</script>

<style></style>
