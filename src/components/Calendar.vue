<template>
  <div class="calendar">
    <div class="header">
      <div class="date__title">{{ currentDate }}</div>
      <div class="date__title">{{ month.toLocaleString('uk-UA', { month: 'long' }).toUpperCase() }}</div>
      <month-switcher :date="month" @update:date="updateMonth" />
    </div>
    <table class="calendar__content">
      <thead>
      <tr>
        <th>Понеділок</th>
        <th>Вівторок</th>
        <th>Середа</th>
        <th>Четвер</th>
        <th>П'ятниця</th>
        <th>Субота</th>
        <th>Неділя</th>
      </tr>
      </thead>
      <tbody>
      <tr v-for="week in weeks" :key="week[0].toString()" class="event_name">
        <td v-for="day in week" :key="day.toString()" :class="{ today: isToday(day), event: isEvent(day) }" @click="handleDateClick(day)">
          {{ day.getDate() }}
        </td>
      </tr>
      </tbody>
    </table>
    <div v-if="showEventTime">
      <event-time />
    </div>
  </div>
</template>
<script>
import MonthSwitcher from './MonthSwitcher.vue';
import EventTime from "@/components/EventTime";
export default {
  name: 'Calendar',
  components: {
    MonthSwitcher,
    EventTime
  },
  data() {
    return {
      month: new Date(),
      eventDate: new Date('2023-03-26T14:00:00.000+02:00'), // Київський час
      showEventTime: false,
      activeDate: new Date(),
    };
  },
  created() {
    this.activeDate = new Date();
  },
  computed: {
    weeks() {
      const firstDayOfMonth = new Date(this.month.getFullYear(), this.month.getMonth(), 1);
      const lastDayOfMonth = new Date(this.month.getFullYear(), this.month.getMonth() + 1, 0);
      const firstDayOfWeek = firstDayOfMonth.getDay() === 0 ? 6 : firstDayOfMonth.getDay() - 1;
      const lastDayOfWeek = lastDayOfMonth.getDay() === 0 ? 6 : lastDayOfMonth.getDay() + 5;
      const daysInMonth = lastDayOfMonth.getDate();

      const weeks = [];
      let currentWeek = [];
      let currentDay = 1 - firstDayOfWeek;

      for (let i = 0; i < 6; i += 1) {
        for (let j = 0; j < 7; j += 1) {
          const date = new Date(this.month.getFullYear(), this.month.getMonth(), currentDay);
          currentWeek.push(date);
          currentDay += 1;
          if (currentDay > daysInMonth) break;
        }
        weeks.push(currentWeek);
        currentWeek = [];
        if (currentDay > daysInMonth) break;
      }

      if (lastDayOfWeek < 6) {
        for (let i = lastDayOfWeek + 1; i < 7; i += 1) {
          const date = new Date(this.month.getFullYear(), this.month.getMonth() + 1, 1 + i - lastDayOfWeek);
          currentWeek.push(date);
        }
        weeks.push(currentWeek);
      }

      return weeks;
    },
    currentDate() {
      const options = {
        day: '2-digit',
        month: '2-digit',
        year: 'numeric',
        hour: '2-digit',
        minute: '2-digit',
        timeZone: 'Europe/London',
        timeZoneName: 'short'
      };
      const londonDate = new Date().toLocaleString('en-GB', options);
      return londonDate;
      const option = {
        day: '2-digit',
        month: 'long',
        year: 'numeric',
        hour: '2-digit',
        minute: '2-digit',
        timeZone: 'Europe/Kiev',
        timeZoneName: 'short'
      };
      const kievDate = new Date().toLocaleString('uk-UA', option);
      return kievDate;
    },

  },
  methods: {
    isToday(day) {
      const today = new Date();
      return day.getDate() === today.getDate() &&
          day.getMonth() === today.getMonth() &&
          day.getFullYear() === today.getFullYear();
          day.toDateString() === today.toDateString();
    },
    isEvent(day) {
      return day.getTime() === this.eventDate.getTime();
    },
    handleDateClick(day) {
      console.log(day);
      this.showEventTime = true;
    },
    updateMonth(date) {
      this.month = date;
    },
  },
};
</script>

<style scoped>
.date__title{
  border: 1px solid navy;
  padding: 10px 20px;
  border-radius: 10px;
  background-color: navy;
  font-family: SimSun;
  color: aliceblue;
  font-weight: 700;
  font-size: 15px;
  line-height: 21px;
}

.header {
  display: flex;
  align-items: center;
  margin-left: 250px;
  margin-right: 250px;
  justify-content: space-evenly;
}

.header__container {
 display: flex;
 align-items: center;
 text-align: center;
 margin-left: auto;
 margin-right: auto;
}

.calendar__content {
 margin-left: auto;
 margin-right: auto;
}


th {
  border-bottom: 2px solid rgba(128, 128, 128, 0.55);
}

th, td {
  padding: 20px;
}

.event_name {
  cursor: pointer;
}
.today {
  background-color: navy;
  color: aliceblue;
  font-weight: 700;
  cursor: pointer;
  border-radius: 10px;
}
</style>

