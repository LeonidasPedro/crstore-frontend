<template>
  <v-app dark>
    <v-app-bar
      app
      color="black"
      flat
    >
      <v-avatar
        :color="$vuetify.breakpoint.smAndDown ? 'orange lighten-2' : 'transparent'"
        size="32"
      >
      </v-avatar>
        

      <v-avatar
        class="hidden-sm-and-down"
        color="orange lighten-2 shrink"
        size="32"
      ></v-avatar>
    </v-app-bar>
    <v-img
    src="https://vejasp.abril.com.br/wp-content/uploads/2016/11/6430_pizzariabatepapo-12-jpg.jpeg?quality=70&strip=info&w=1000&resize=1200,800"
    style="max-height: 300px;"
    >
    </v-img>

    <v-main> 
      <v-container>
        <Nuxt />
      </v-container>
    </v-main>
     <v-footer padless>
    <v-col
      class="text-center"
      cols="12"
    >
      {{ new Date().getFullYear() }} — <strong>CRStore</strong>
    </v-col>
  </v-footer>
  </v-app>
</template>

<script>
  export default {
    data: () => ({
      links: [
        'Home',
        'Pedidos',
        'Login',
        'Carrinho'
      ],
      async changePage(){

      }
    }),
  }
</script>