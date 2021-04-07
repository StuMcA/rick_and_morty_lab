<template>
  <section>
      <img :src="character.image" alt="Image of character">
      <h3>{{character.name}}</h3>
      <p>Species: {{ character.species }}</p>
      <p>Status: {{ character.status }}</p>
      <p>Origin Name: {{ character.origin.name }}</p>
  </section>
</template>

<script>

export default {
    name: 'character-detail',
    props: ['character']
}

</script>

<style>

</style>