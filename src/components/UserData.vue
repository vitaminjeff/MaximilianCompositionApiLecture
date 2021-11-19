<template>
   <h2>{{ userName }}</h2>
   <h3>{{ age }}</h3>
</template>

<script>
import { computed } from 'vue';

export default {
   props: ['firstName', 'lastName', 'age'],
   setup() {
      const uName = computed(function() {
         return this.firstName + ' ' + this.lastName; // not the same access to `this`
      });

      return { userName: uName};
   }
};
</script>
