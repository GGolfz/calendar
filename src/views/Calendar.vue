<template>
  <v-row>
    <v-col
      cols="2"
      :class="hover1 ? `title2 active` : `title2`"
      @click="goto(year + 542)"
      @mouseover="hover1 = true"
      @mouseleave="hover1 = false"
    >
      {{ year + 542 }}
    </v-col>
    <v-col cols="8" class="title1">
      {{ year + 543 }}
    </v-col>
    <v-col
      cols="2"
      :class="hover2 ? `title2 active` : `title2`"
      style="text-align:end"
      @click="goto(year + 544)"
      @mouseover="hover2 = true"
      @mouseleave="hover2 = false"
    >
      {{ year + 544 }}
    </v-col>
    <v-col cols="12">
      <Subcalendar :index="calculateIndex()" />
    </v-col>
  </v-row>
</template>

<script>
import Subcalendar from '../components/Subcalendar'
export default {
  components: {
    Subcalendar
  },
  data() {
    return {
      year: '',
      isLeap: false,
      index: 0,
      hover1: false,
      hover2: false
    }
  },
  async mounted() {
    await this.getData()
  },
  methods: {
    async getData() {
      this.year = (await this.$route.params.year) - 543
      this.isLeap = await this.checkLeap()
      this.index = await this.calculateIndex()
    },
    async checkLeap() {
      if (this.year % 4 == 0) {
        if (this.year % 100 != 0) {
          return true
        } else {
          if (this.year % 400 == 0) {
            return true
          }
        }
      }
      return false
    },
    calculateIndex() {
      let a = Math.floor(this.year / 100)
      let b = this.year % 100
      if (!this.isLeap) {
        return ((7 + 5 * (a % 4) + 5 * Math.floor(b / 4) + (b % 4)) % 7) + 1
      } else {
        return ((6 + 5 * (a % 4) + 5 * Math.floor(b / 4) + (b % 4)) % 7) + 8
      }
    },
    async goto(year) {
      await this.$router.push(`/calendar/${year}`)
      await this.getData()
    }
  }
}
</script>

<style>
.title1 {
  text-align: center;
  font-size: 2em;
  cursor: default;
}
.title2 {
  font-size: 1.5em;
  opacity: 0.5;
  cursor: pointer;
  transition: 1s;
}
.active {
  opacity: 1 !important;
}
</style>
