<template>
  <ul>
      <character-item v-for="(character, index) in characterList.results" :character="character" :key="index"/>
  </ul>
</template>

<script>
import characterItem from './characterItem'

export default {
    name: 'character-list',

    props: ['characterList'],

    components: {
        "character-item": characterItem
    },

    methods: {
        
    }
}
</script>

<style scoped>

</style>