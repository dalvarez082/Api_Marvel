<template>
  <v-app dark>     
    <v-main>
      <v-container>
        <Nuxt />
      </v-container>
    </v-main>
  </v-app>
</template>

<script>

export default {  
  async asyncData() {    
  },
  name: 'DefaultLayout',
  data() {
    return {
      clipped: false,
      drawer: false,
      fixed: false,
      items: [ ],
      miniVariant: false,
      right: true,
      rightDrawer: false,
      title: 'Api Marvel',
    }
  },
}

</script>
