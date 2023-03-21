<template>
  <div class="app">
    <div class="container">
      <calendar class="app__container"/>
    </div>
  </div>
</template>

<script>
import Calendar from '@/components/Calendar';
export default {
  components: {Calendar}
}

</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.app {
  padding-top: 20px;
}

.container {
  text-align: center;
}

</style>
