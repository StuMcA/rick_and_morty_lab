<template>
  <li @click="handleClick">{{character.name}}</li>
</template>

<script>

import { eventBus } from '../main.js';

export default {
  name: 'character-item',
  props: ['character'], 
  methods: {
      handleClick: function() {
        eventBus.$emit('send-character', this.character)
    },
  }
}
</script>

<style scoped>
li {
    list-style: none;
    cursor: pointer;
}

</style>>

