<template>
  <section class="container">
    <h2>{{ userName }}</h2>
  </section>
</template>

<script>
import { ref } from 'vue';

export default {
  setup() {
    // this - does not refer to the Vue config object inside here like it does in methods
    // ref(); // returns reference to a reactive value, not to a DOM thing
    let uName = ref('Maximilian');

    setTimeout(function () {
      uName = 'Max';
    }, 2000);

    return {
      userName: uName
    };
  }
  // data() {
  //   return {
  //     userName: 'Maximilian',
  //   };
  // },
};
</script>

<style>
* {
  box-sizing: border-box;
}

html {
  font-family: sans-serif;
}

body {
  margin: 0;
}

.container {
  margin: 3rem auto;
  max-width: 30rem;
  border-radius: 12px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
  padding: 1rem;
  text-align: center;
}
</style>