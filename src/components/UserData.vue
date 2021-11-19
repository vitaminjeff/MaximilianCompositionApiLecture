<template>
   <div>
      <h2>{{ userName }}</h2>
      <h3>{{ age }}</h3>
   </div>
</template>

<script>
import { computed } from 'vue';

export default {
   props: ['firstName', 'lastName', 'age'],
   setup(props, context) {
      const uName = computed(function() {
         // return this.firstName + ' ' + this.lastName; // not the same access to `this`
         return props.firstName + ' ' + props.lastName; // not the same access to `this`
      });

      console.log(context); // attrs, emit, slots

      return { userName: uName };
   }
};
</script>
