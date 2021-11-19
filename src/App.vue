<template>
  <section class="container">
    <user-data :first-name="firstName" :last-name="lastName" class="test"></user-data>
    <button @click="setAge">Change Age</button>
    <div>
      <input type="text" placeholder="First Name" v-model="firstName" />
      <input type="text" placeholder="Last Name" ref="lastNameInput" />
      <button @click="setLastName">Set Name</button>
    </div>
  </section>
</template>

<script>
import { ref,  reactive, /* isRef, isReactive, toRefs */ computed, watch, provide } from 'vue';
import UserData from './components/UserData.vue';

export default {
  components: {
    UserData
  },
  setup() {
    // this - does not refer to the Vue config object inside here like it does in methods
    // ref(); // returns reference to a reactive value, not to a DOM thing
    // const uName = ref('Maximilian');
    const firstName = ref('');
    const lastName = ref('');
    const lastNameInput = ref(null); // no differentiation between your own refs and refs you want to bind to a DOM element
    const uAge = ref(31);
      
    provide('userAge', uAge); // places where you inject the uAge ref will automatically be updated

    // uName.value is a readonly ref
    // uName.Value = 'NOPE!'; // can't do this
    const uName = computed(function() {
      return firstName.value + ' ' + lastName.value;
    });

    // single dependency
    // watch(uAge, function(newValue, oldValue) {
    //   console.log('Old age: ' + oldValue)
    //   console.log('New age: ' + newValue)
    // });
    watch([uAge, uName], function(newValues, oldValues) { // arguments are now arays
      console.log('Old age: ' + oldValues[0])
      console.log('New age: ' + newValues[0])
      console.log('Old name: ' + oldValues[1])
      console.log('New name: ' + newValues[1])
    });

    // reactive is like ref, but it's made for only for objects
    const user = reactive({
      name: 'Maximilian',
      age: 31
    });

    function setNewAge() {
      // user.age = 32
      uAge.value = 33;
    }

    function setLastName() {
      // lastName.value = this.$refs.lastNameInput.value; // no access to this
      lastName.value = lastNameInput.value.value; // access .value property of ref which is a pointer to <input /> element w/ a .value property
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
      userName: uName,
      userAge: uAge,
      setAge: setNewAge,
      firstName,
      lastName,
      lastNameInput,
      setLastName
    };
  },
  // data() {
  //   return {
  //     userName: 'Maximilian',
  //   };
  // },
  // the options api way of doing provide/inject
  // provide() {
  //    return { age: this.age };
  // }
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