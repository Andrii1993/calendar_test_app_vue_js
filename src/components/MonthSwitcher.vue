<template>
  <div className="btn__container">
    <button @click="prevMonth" class="btn_prev">Prev</button>
    <button @click="nextMonth" class="btn_next">Next</button>
  </div>
</template>

<script>
export default {
  name: 'MonthSwitcher',
  props: {
    date: {
      type: Date,
      default: () => new Date(),
    },
  },
  methods: {
    prevMonth() {
      const prevMonthDate = new Date(this.date.getFullYear(), this.date.getMonth() - 1, 1);
      this.$emit('update:date', prevMonthDate);
    },
    nextMonth() {
      const nextMonthDate = new Date(this.date.getFullYear(), this.date.getMonth() + 1, 1);
      this.$emit('update:date', nextMonthDate);
    },
  },
};

</script>

<style scoped>
  .btn__container {
    margin-top: 10px;
    margin-bottom: 10px;
  }

  .btn_prev {
    border: none;
    padding: 10px 20px;
    border-top-left-radius: 10px;
    border-bottom-left-radius: 10px;
    background-color: navy;
    font-family: SimSun;
    color: aliceblue;
    font-weight: 700;
    font-size: 15px;
    line-height: 21px;
    cursor: pointer;
  }

  .btn_next{
    border: none;
    padding: 10px 20px;
    border-top-right-radius: 10px;
    border-bottom-right-radius: 10px;
    background-color: navy;
    font-family: SimSun;
    color: aliceblue;
    font-weight: 700;
    font-size: 15px;
    line-height: 21px;
    cursor: pointer;
  }
</style>