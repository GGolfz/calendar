<template>
  <v-card style="height:400px;cursor:default">
    <v-row>
      <v-col cols="12" style="text-align:end;padding:4% 8% 0% 8%;">
        {{ monthlist[months.month - 1] }}
      </v-col>
      <v-col cols="12">
        <v-row class="calen1">
          <v-col
            class="col1"
            v-for="(i, index) in days"
            :key="index"
            :style="`color:${dayc[index]};font-weight:bold`"
            >{{ i }}</v-col
          >
          <v-col cols="12">
            <v-row v-for="(i, index) in daylist" :key="index">
              <v-col class="col1" v-for="(j, id1) in i" :key="id1">
                {{ j }}
              </v-col>
            </v-row>
          </v-col>
        </v-row>
      </v-col>
    </v-row>
  </v-card>
</template>

<script>
export default {
  data() {
    return {
      days: ['Sun', 'Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat'],

      dayc: [
        '#FF6961',
        '#FDE26C',
        '#FF9AA2',
        '#89E894',
        '#FFB347',
        '#80E2FF',
        '#BA9FE7'
      ],
      daylist: [],
      monthlist: [
        'January',
        'February',
        'March',
        'April',
        'May',
        'June',
        'July',
        'August',
        'September',
        'October',
        'November',
        'December'
      ]
    }
  },
  props: {
    months: {
      month: Number,
      start: Number,
      end: Number
    }
  },
  mounted() {
    this.render()
  },
  watch: {
    months() {
      this.render()
    }
  },
  methods: {
    render() {
      this.daylist = []
      for (
        let i = 0;
        i < Math.ceil((this.months.end + this.months.start) / 7) * 7;
        i++
      ) {
        if (i % 7 == 0) {
          this.daylist.push([])
        }
        if (
          i < this.months.start ||
          i > this.months.end + this.months.start - 1
        ) {
          this.daylist[Math.floor(i / 7)].push('')
        } else {
          this.daylist[Math.floor(i / 7)].push(i - this.months.start + 1)
        }
      }
    }
  }
}
</script>

<style>
.col1 {
  width: 14.29%;
  font-size: 0.8em;
  text-align: center;
}
.calen1 {
  padding: 2%;
}
</style>
