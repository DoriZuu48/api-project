<template>
  <div class="home">
    rick and morty
    <character-block 
    v-for="character in characters" 
    :key="character.id"
    :character="character"
    />
  </div>
</template>

<script>

import characterBlock from '@/components/characterBlock.vue';
//import characterBlock from '../components/characterBlock.vue';

export default {
  components: { characterBlock },
  name: 'Home',
  component: {
    characterBlock
 },
  data() {
    return {
      currentPage: 1, 
    }
  },

  created() {
    this.$store.dispatch('fetchCharacters', this.currentPage);
  },
  computed: {
    characters() {
        return this.$store.getters['getCharactersByPage'](this.currentPage);
     },
    firstCharacter() {
      return this.$store.getters['getCharacterById']({id: 1, page:1});
    }
  },
}

</script>
