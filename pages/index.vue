<template>
  <div class="container">
    <div class="segment-one">   
      <h2>Personajes de marvel</h2>   
      <v-slide-group>
        <v-slide-item v-for="(character, index) in characters" :key="index">
          <div class="character-card" @click="showDescription(character)">
            <img :src="character.thumbnail.path + '/portrait_fantastic.' + character.thumbnail.extension" alt="Character image">
            <p>{{ character.name }}</p>
          </div>
        </v-slide-item>
      </v-slide-group>
    </div>
    <div class="segment-two">
      <div class="left">
        <h2>{{ selectedCharacter.name }}</h2>
        <img :src="selectedCharacter.thumbnail.path + '/portrait_fantastic.' + selectedCharacter.thumbnail.extension" alt="Character image">
      </div>
      <div class="right">
        <p>Comics: {{ selectedCharacter.comics.available }}</p>
        <p>Series: {{ selectedCharacter.series.available }}</p>
        <p>Stories: {{ selectedCharacter.stories.available }}</p>
        <p>Events: {{ selectedCharacter.events.available }}</p>
        <p>{{ selectedCharacter.description ? selectedCharacter.description : 'Este personaje es obtenido de la API de Marvel. Algunos personajes pueden no tener descripción, pero podrás encontrar información sobre sus cómics, series, historias y eventos en los que ha aparecido. ¡Explora el universo de Marvel y disfruta!' }}
        </p>
      </div>
</div>
    <div class="segment-three">
      <h2>Series del personaje seleccionado</h2>
      <ul>
        <li v-for="(serie, index) in series" :key="index">
          <img :src="serie.thumbnail.path + '/portrait_fantastic.' + serie.thumbnail.extension" alt="Serie image">
          <p>{{ serie.title }}</p>
        </li>
      </ul>
    </div>
  </div>
</template>


<script>
  export default {
    data() {
      return {
        characters: [],
        selectedCharacter: {
          name: '',
          thumbnail: {
            path: '',
            extension: ''
          },
          comics: { available: 0 },
          series: { available: 0 },
          stories: { available: 0 },
          events: { available: 0 },
          description: ''
        },
        series: []
      }
    },
    async mounted() {
      const response = await this.$axios.$get('characters', { params: { apikey: 'ad6bdd113a25813549da8c25b33f1997' }})
      this.characters = response.data.results
      console.log(response)
      if (this.characters.length > 0) {
        await this.showDescription(this.characters[0])
      }
    },
    methods: {
      async showDescription(character) {
        const response = await this.$axios.$get(`characters/${character.id}`, { params: { apikey: 'ad6bdd113a25813549da8c25b33f1997' }})
        this.selectedCharacter = response.data.results[0]
        const seriesResponse = await this.$axios.$get(`characters/${character.id}/series`, { params: { apikey: 'ad6bdd113a25813549da8c25b33f1997', limit: 3 }})
        this.series = seriesResponse.data.results
      }
    }
  }
</script>


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
  display: flex;
  flex-wrap: wrap;
  align-items: center;
}

.segment-two .left {
  flex: 1 1 40%;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.segment-two .left img {
  max-width: 100%;
  height: auto;
}

.segment-two .right {
  flex: 1 1 60%;
  display: flex;
  flex-direction: column;
  justify-content: center;
}

.segment-two h2 {
  margin-top: 0;
}

.segment-two p {
  margin: 0;
  margin-bottom: 10px;
}

.segment-three {
  flex: 1 1 50%;
  background-color: #b716c3;
  height: 50%;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.segment-three h2 {
  margin-top: 0;
}

.segment-three ul {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  align-items: center;
  margin: 0;
  padding: 0;
}

.segment-three ul li {
  flex: 1;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 80%;
  padding: 20px;
  text-align: center;
  list-style-type: none;
  margin: 5px;
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




  
  