<template>
  <section class="container">
    <h2>{{ user.name }}</h2>
    <h3>{{ user.age }}</h3>
    <button @click="setAge">Change Age</button>
  </section>
</template>

<script>
import { /*ref, */ reactive, /* isRef, isReactive, toRefs */ } from 'vue';

export default {
  setup() {
    // this - does not refer to the Vue config object inside here like it does in methods
    // ref(); // returns reference to a reactive value, not to a DOM thing
    // const uName = ref('Maximilian');
    // const uAge = ref(31);

    // reactive is like ref, but it's made for only for objects

    const user = reactive({
      name: 'Maximilian',
      age: 31
    });

    function setNewAge() {
      user.age = 32
    }

    // console.log(uAge, user);

    // console.log(uAge.value); // just a snapshot, no value watcher
    // console.log(user.name, user.age); // just a snapshot, no value watcher

    // console.log(isRef(uAge.value)); // check if ref
    // console.log(isReactive(user.name), user.age); // check if reactive

    // console.log(isRef(uAge)); // check if ref
    // console.log(isReactive(user)); // check if reactive

    // setTimeout(function () {
    //   user.name = 'Max';
    //   user.age = 32;
    // }, 2000);

    // const userRefs = toRefs(user); // get back an object whose properties are refs

    return {
      user: user,
      // userName: userRefs.name,
      // age: userRefs.age
      setAge: setNewAge
    };
  },
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