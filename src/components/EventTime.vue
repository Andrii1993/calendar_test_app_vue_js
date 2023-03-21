<template>
  <div class="event__time">
    <div>Дата: {{ eventDate.toLocaleDateString('uk-UA') }}</div>
    <div>Час: {{ eventDate.toLocaleTimeString('uk-UA', {timeZone: 'Europe/Kiev'}) }} - {{ endDateTime.toLocaleTimeString('uk-UA', {timeZone: 'Europe/Kiev'}) }}</div>
  </div>
</template>

<script>
export default {
  name: 'EventTime',
  data() {
    return {
      eventDate: new Date('2023-03-26T13:00:00.000+02:00'), // Київський час
      duration: 60, // тривалість події в хвилинах
    };
  },
  computed: {
    endDateTime() {
      return new Date(this.eventDate.getTime() + this.duration * 60 * 1000);
    },
  },
};
</script>
<style scoped>
  .event__time {
    margin-top: 20px;
    margin-left: 350px;
    margin-right: 350px;
    padding: 10px 20px;
    border-radius: 10px;
    background-color: navy;
  }

  .event__time div {
    font-family: SimSun;
    color: aliceblue;
    font-weight: 700;
    font-size: 15px;
    line-height: 21px;
    cursor: pointer;
  }
</style>