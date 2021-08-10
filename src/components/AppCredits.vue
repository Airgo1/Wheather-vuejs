<template>
  <footer>
    <small>© <b>Burdet Nicolas</b> {{ year }} - A exemple Project</small>
  </footer>
</template>

<script>
export default {
  name: 'AppCredits',

  props: {
    year: {
      type: Number,
      required: true
    }
  }
}
</script>

<style scoped>
footer {
  text-align: center;
  position: relative;
  visibility: hidden;
}

.app--day {
    background-image: linear-gradient(rgba(0, 0, 0, 0.1), rgba(0, 0, 0, 0.1)), url('../assets/images/morning.jpg');
}

.app--night {
    background-image: linear-gradient(rgba(0, 0, 0, 0.1), rgba(0, 0, 0, 0.1)), url('../assets/images/night.jpg');
}

@media screen and (min-width: 450px) {
  footer {
    visibility: visible;
  }
}
</style>
