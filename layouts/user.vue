<template>
  <v-app id="inspire">
    <v-app-bar
      app
      color="white"
      flat
    >
      <v-container class="py-0 fill-height">
        <v-avatar
          class="mr-10"
          color="grey darken-1"
          size="32"
        ></v-avatar>

        <v-btn
          v-for="(item, i) in items"
          :key="i"
          text
          :to="item.to"
        >
          {{ item.title }}
        </v-btn>

        <v-spacer></v-spacer>
      </v-container>
    </v-app-bar>

    <v-main class="grey lighten-3">
      <v-container>
       <Nuxt />
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
  export default {
    data: () => ({
      items:[
        {
          title:'Home',
          to:'/'
        },
        {
          title:'Pedidos',
          to:'/erro'
        },
        {
          title:'login',
          to:'/user/'
        },
        {
          title:'Carrinho',
          to:'/erro'
        },
        {
          title:'Endereços',
          to:'/adresses'
        },

      ]
    }),
  }
</script>