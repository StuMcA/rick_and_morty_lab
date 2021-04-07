<template>
  <div id="app">
    <h1>Character List</h1>
    <div class="main-container">
      <form @submit.prevent="typeCharacter">
        <label for="character-name-search">Enter character name:</label>
        <input type="text" id="character-name-search" v-model="searchedCharacter">
      </form>

<!-- event.preventDefault(); -->

      <label for="character_select">Select a Character:</label>
      <select id="character_select" v-model="selectedCharacter">
        <option disabled value="">Select a character</option>
        <option v-for="character in characterList.results" :key="character.name" :value="character">{{character.name}}</option>
      </select>

      <!-- <character-list :characterList='characterList'></character-list> -->

      <character-detail v-if="selectedCharacter" :character="selectedCharacter" />

    </div>
  </div>
</template>

<script>

import {eventBus} from './main.js';

import characterList from './components/characterList.vue';
import characterDetail from './components/characterDetail.vue'

export default {
  name: 'App',

    data(){
    return {
      characterList: [],
      selectedCharacter: null,
      searchedCharacter: null
    };
  },

  mounted(){
    fetch('https://rickandmortyapi.com/api/character/')
    .then(res => res.json())
    .then(characterList => this.characterList = characterList)

    eventBus.$on('send-character', (character) => {
    //  console.log("event triggered", character)
     this.selectedCharacter = character;
    })
  },

  components: {
    'character-list': characterList,
    'character-detail': characterDetail
  },

  methods: {
    typeCharacter: function(event) {
      event.preventDefault();
      // Take text entered
      let characterInput = this.searchedCharacter
      // Search list of characters
        for (let character of this.characterList.results) {
          if (character.name === (characterInput)) {
              this.selectedCharacter = character
          }
        }
    }
  }
}

</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.main-container {
  /* display: grid;
  justify-content: space-between; */
}
</style>
