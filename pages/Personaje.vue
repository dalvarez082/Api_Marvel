<template>
    <div class="container">
      <h1>Personajes de Marvel</h1>
      <div class="characters">
        <div v-for="character in characters" :key="character.id" class="character">
          <div class="overlay"></div>
          <img :src="character.thumbnail.path + '/portrait_fantastic.' + character.thumbnail.extension" :alt="'Imagen de ' + character.name" />
          <h2>{{ character.name }}</h2>
        </div>
      </div>
    </div>
  </template>
  <style>
  .container {
    max-width: 1000px;
    margin: 0 auto;
    padding: 20px;
  }
  
  .characters {
    display: flex;
    overflow-x: scroll;
    scroll-behavior: smooth;
  }
  
  .character {
    position: relative;
    margin-right: 20px;
    cursor: pointer;
  }
  
  .character img {
    width: 200px;
    height: 300px;
    object-fit: cover;
  }
  
  .character .overlay {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.5);
    opacity: 0;
    transition: opacity 0.3s ease-in-out;
  }
  
  .character:hover .overlay {
    opacity: 1;
  }
  
  .character h2 {
    position: absolute;
    bottom: 0;
    left: 0;
    padding: 10px;
    margin: 0;
    font-size: 16px;
    color: #fff;
    text-shadow: 1px 1px 2px rgba(0, 0, 0, 0.8);
  }
  </style>
  
  <script>

  
  export default {
    data() {
      return {
        characters: []
      }
    },
    async mounted() {
        console.log(this)
      const response = await this.$axios.$get('characters',{params:{
        apikey: 'ad6bdd113a25813549da8c25b33f1997'}})
      this.characters = response.data.results
      console.log(this.characters)
    }
  }
  </script>
  
  