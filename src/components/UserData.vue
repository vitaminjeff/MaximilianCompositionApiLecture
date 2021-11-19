<template>
   <div>
      <h2>{{ userName }}</h2>
      <h3>{{ age }}</h3>
   </div>
</template>

<script>
import { computed, inject } from 'vue';

export default {
   // inject: [], // this is the old way
   props: ['firstName', 'lastName'],
   setup(props, context) {
      const uName = computed(function() {
         // return this.firstName + ' ' + this.lastName; // not the same access to `this`
         return props.firstName + ' ' + props.lastName; // not the same access to `this`
      });

      const age = inject('userAge'); // use the same key as where you provide
      // age.value = 32; // don't do this, only change injected values in the place where you provide them from

      console.log(context); // attrs, emit, slots

      // this.$emit(); // can't do this outside of options api
      // context.emit('save-data', 1);

      return { userName: uName, age };
   }
};
</script>
