<template>
  <div>
    <div>{{ month }}</div>
    <table>
      <thead>
      <tr>
        <th>Mon</th>
        <th>Tue</th>
        <th>Wed</th>
        <th>Thu</th>
        <th>Fri</th>
        <th>Sat</th>
        <th>Sun</th>
      </tr>
      </thead>
      <tbody>
      <tr v-for="week in weeks" :key="week[0].getTime()">
        <td v-for="day in week" :key="day.getTime()">
          {{ day.getDate() }}
        </td>
      </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  name: 'Calendar',
  props: {
    date: {
      type: Date,
      default: () => new Date(),
    },
  },
  computed: {
    month() {
      return this.date.toLocaleDateString('default', { month: 'long' });
    },
    weeks() {
      const firstDayOfMonth = new Date(this.date.getFullYear(), this.date.getMonth(), 1);
      const lastDayOfMonth = new Date(this.date.getFullYear(), this.date.getMonth() + 1, 0);
      const firstDayOfCalendar = new Date(
          firstDayOfMonth.getFullYear(),
          firstDayOfMonth.getMonth(),
          firstDayOfMonth.getDate() - firstDayOfMonth.getDay()
      );
      const lastDayOfCalendar = new Date(
          lastDayOfMonth.getFullYear(),
          lastDayOfMonth.getMonth(),
          lastDayOfMonth.getDate() + (6 - lastDayOfMonth.getDay())
      );
      const weeks = [];
      let currentDay = new Date(firstDayOfCalendar);
      while (currentDay <= lastDayOfCalendar) {
        const week = [];
        for (let i = 0; i < 7; i++) {
          week.push(new Date(currentDay));
          currentDay.setDate(currentDay.getDate() + 1);
        }
        weeks.push(week);
      }
      return weeks;
    },
  },
};
</script>

<style scoped>

</style>
