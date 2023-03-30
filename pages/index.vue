<template>
  <div class="container">
    <div class="segment-one">   
      <h2>Personajes de marvel</h2>   
      <v-slide-group>
        <v-slide-item v-for="(character, index) in characters" :key="index">
          <div class="character-card">
            <img :src="character.thumbnail.path + '/portrait_fantastic.' + character.thumbnail.extension" alt="Character image">
            <p>{{ character.name }}</p>
          </div>
        </v-slide-item>
      </v-slide-group>
    </div>
    <div class="segment-two">
      <h2>Segment Two</h2>
    </div>
    <div class="segment-three">
      <h2>Segment Three</h2>
    </div>
  </div>
</template>

<style>

html,
  body {
    height: 100%;
    margin: 0;
    padding: 0;
  }

  .container {
    display: flex;
    flex-wrap: wrap;
    height: 100%;
    width: 100%;
    max-width: 100%;
    box-sizing: border-box;
   
  }

  .segment-one {
    
    background-color: #b82626;
    height: 50%;    
    align-items: flex-start;
    overflow: hidden;
    
  }
  .segment-one h2 {
    text-align: center; /* Centra horizontalmente el título */
  }

  .segment-two {
    flex: 1 1 50%;
    background-color: #15cf78;
    height: 50%;
  }

  .segment-three {
    flex: 1 1 50%;
    background-color: #b716c3;
    height: 50%;
  }

  



  
  .v-slide-group {
    display: flex;
    justify-content: center;
    margin-top: 1%;
    
    
    width: 100%; /* Ajusta el ancho del componente al 80% del ancho de su contenedor padre */
  }

.character-card {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    height: 80%;
    padding: 20px;
    text-align: center;

}

.character-card img {
  width: 100%;
  height: 100%;
  object-fit: cover;
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
      const response = await this.$axios.$get('characters', { params: { apikey: 'ad6bdd113a25813549da8c25b33f1997' }})
      this.characters = response.data.results
      console.log(response)
    }
  }
</script>




  
  