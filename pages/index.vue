<template>
  <v-container>
    <h1>CRStore</h1>
    <hr>
    <v-container>
      <v-row>
        <v-col>
  
        </v-col>
        <v-col
            cols="4"
          >
            <v-autocomplete
              v-model="items.id"
              :items="categories"
              outlined
              label="Categoria"
              item-text="name"
              item-value="id"
              required
              :rules="rule"
            ></v-autocomplete>
          </v-col>
      </v-row>
    </v-container>
    <v-container>
      <v-card
       v-for="item in items"
       :key="item.id"
       class="mx-auto"
       max-width="344"
      >
      <p></p>
      <v-img
        src="https://images2.nogueirense.com.br/wp-content/uploads/2021/11/pizza-de-calabresa-em-cima-da-mesa_140725-5396-1626098384-1629145531-1636147051-600x417.jpg"
        height="200px"
      > 
      </v-img>

      <v-card-title>
        {{item.name}}
      </v-card-title>

      <v-card-subtitle>
        R${{item.price}}
      </v-card-subtitle>

      <v-card-actions>
      <v-btn
        color="orange lighten-2"
        text
      >
        Adicionar ao Carrinho
        </v-btn>

        <v-spacer></v-spacer>
        </v-card-actions>

        <v-expand-transition>
        <div v-show="show">
        <v-divider></v-divider>

        <v-card-text>
          I'm a thing. But, like most politicians, he promised more than he could deliver. You won't have time for sleeping, soldier, not with all the bed making you'll be doing. Then we'll go with that data file! Hey, you add a one and two zeros to that or we walk! You're going to do his laundry? I've got to find a way to escape.
        </v-card-text>
      </div>
    </v-expand-transition>
  </v-card>
    </v-container>
  </v-container>
</template>

<script>
export default {
  name: 'ItemsPage',
  data () {
    return {
      items: [],
      categories: []
    }
  },
  created () { //executado toda vez que a pagina é carregada
    this.getItems()
    this.getCategories();
  },
  methods: {
     async getCategories () {
      let response = await this.$axios.$get('http://localhost:3333/categories');
      this.categories = response.data
     console.log(this.categories);
    },
    async getItems () {
      let response = await this.$axios.$get('http://localhost:3333/items');
      this.items = response.data
      console.log(this.items);
      
    },
  },

}
</script>
