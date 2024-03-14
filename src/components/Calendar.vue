<template>
  <div class="container mx-auto mb-5">
    Календарь
    <div class="section flex justify-center mb-10">
      <div class="flex month mr-5">
        <button class="left"><-</button>
        <div class="px-4">{{ getMonth }}</div>
        <button class="right" @click="getNextMonth">+></button>
      </div>
      <div class="flex year">
        <button class="left"><-</button>
        <div class="px-4">{{ getYear }}</div>
        <button class="right" @click="getNextYear">+></button>
      </div>
    </div>
    <div class="container mx-auto flex flex-wrap">
      <div
        class="days item cursor-pointer text-center py-3 bg-green-100 border"
        v-for="(day, index) in weekday"
        :key="index"
      >
        {{ day }}
      </div>
      <div
        class="item bg-green-50 border cursor-pointer text-center py-5"
        v-for="i in result"
      >
        {{ i }}
      </div>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      weekday: [
        "понедельник",
        "вторник",
        "среда",
        "четврег",
        "пятница",
        "суббота",
        "воскресенье",
      ],
      longMonth: [
        "январь",
        "февраль",
        "март",
        "апрель",
        "май",
        "июнь",
        "июль",
        "август",
        "сентябрь",
        "октябрь",
        "ноябрь",
        "декабрь",
      ],
      year: new Date().getFullYear(),
      month: new Date().getMonth(),
      days: [],
    };
  },
  methods: {
    getNextYear() {
      this.year = this.year + 1;
    },
    getNextMonth() {
      if (this.month <= 11) {
        this.month = this.month + 1;
      }
      if (this.month == 12) {
        this.month = 0;
        this.year = this.year + 1;
      }
    },
  },
  computed: {
    result() {
      this.days = [];
      for (let i = this.firstDayIdx; i < this.getDaysOfMonth + this.firstDayIdx; i++) {
        this.days[i] = i + 1 - this.firstDayIdx;
      }
      return this.days;
    },
    getDaysOfMonth() {
      return new Date(this.year, this.month + 1, 0).getDate();
    },
    getMonth() {
      return this.longMonth[this.month];
    },
    getYear() {
      console.log();
      return this.year;
    },
    firstDayIdx() {
      return new Date(this.year, this.month, 1).getUTCDay();
    },
  },
};
</script>
<style>
.item {
  width: calc(100% / 7);
}
</style>
