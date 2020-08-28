<template>
  <v-row>
    <v-col cols="12" class="titl">
      CALENDAR
    </v-col>
    <v-col cols="12" class="card">
      <v-card>
        <v-row class="pa-6">
          <v-col cols="12">
            <v-text-field label="Year" v-model="year" @keyup.enter="goto()" />
          </v-col>
          <v-col cols="12" style="display:flex;justify-content:flex-end">
            <v-btn @click="goto()">SEARCH</v-btn>
          </v-col>
        </v-row>
      </v-card>
    </v-col>
  </v-row>
</template>

<script>
export default {
  name: 'Home',
  data() {
    return {
      year: ''
    }
  },
  methods: {
    goto() {
      if (parseInt(this.year) > 0) {
        this.$router.push(`/calendar/${this.year}`)
      } else {
        alert('Year must be number more than 0')
      }
    }
  }
}
</script>
<style scoped>
.titl {
  font-size: 2.5em;
  font-weight: bold;
  text-align: center;
}
.card {
  padding: 5% 35%;
}
</style>
