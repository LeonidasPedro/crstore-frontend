<template>
  <v-container>
    <v-container>
      <v-toolbar
      dark
      prominent
      src="https://vejasp.abril.com.br/wp-content/uploads/2016/11/6430_pizzariabatepapo-12-jpg.jpeg?quality=70&strip=info&w=1000&resize=1200,800"
    >
      <v-app-bar-nav-icon></v-app-bar-nav-icon>
      <v-toolbar-title>CRStore</v-toolbar-title>
      
      <v-spacer></v-spacer>
    </v-toolbar>
    </v-container>
    <v-container>
      <v-row>
         <v-col
            cols="4"
          >
            <v-autocomplete
              @change="getByCategory"
              style="margin-top: 50px;"
              v-model="category.id"
              :items="categories"
              outlined
              label="Categoria"
              item-text="name"
              item-value="id"
              required
            ></v-autocomplete>
          </v-col>
          <v-col
            cols="15"
          >
            <v-autocomplete
              @change="getById"
              style="margin-top: 50px;"
              v-model="item.id"
              :items="items"
              outlined
              label="Pesquisar"
              item-text="name"
              item-value="id"
              required
            ></v-autocomplete>
          </v-col>
      </v-row>
    </v-container>
    <v-container>
      <v-row>
            <v-card
            v-for="item in items"
            style="margin-top: 30px;
            margin"
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
            </div>
            </v-expand-transition>
            </v-card>
        <v-card
        v-for="item in search"
        style="margin-top: 30px;
        margin"
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
        </div>
        </v-expand-transition>
        </v-card>
      </v-row>
    </v-container>
  </v-container>
</template>

<script>
export default {
  name: 'ItemsPage',
  data () {
    return {
      category:{
        id:null
      },
      item:{
        id:null
      },
      items:[],
      categories: [],

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
    },
    async getItems () {
      let response = await this.$axios.$get('http://localhost:3333/items');
      this.items = response.data
    },
    async getByCategory(){
      let id = {
        idCategory:this.category.id
      }
      let response = await this.$axios.$post(`http://localhost:3333/items/category/`, id);
      this.items = response.data
    },
    async getById(){
      let id = this.item.id
      console.log(id);
      let response = await this.$axios.$get(`http://localhost:3333/items/${id}`, );
      this.items = []
      this.items.push(response)
    }

  },

}
</script>
