<template>
  <v-container>
    <v-container>
      <v-row style="margin-top: -8%">
         <v-col
            cols="4"
          >
            <v-autocomplete
              @change="getByCategory"
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
            style="margin-top: 30px;"
            :key="item.id"
            class="mx-auto"
            max-width="344"
            >
            <p></p>
            <v-img
            :src="item.thumbnail"
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
              @click="addToCart"
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
  layout:'user',
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
      cart:[]
    }
  },
  created () { //executado toda vez que a pagina é carregada
    this.getItems()
    this.getCategories();
  },
  methods: {
     async getCategories () {
      let response = await this.$api.$get('/categories');
      this.categories = response.data
    },
    async getItems () {
      let response = await this.$api.$get('/items');
      this.items = response.data
    },
    async getByCategory(){
      let id = {
        idCategory:this.category.id
      }
      let response = await this.$api.$post(`/items/category/`, id);
      this.items = response.data
    },
    async getById(){
      let id = this.item.id
      console.log(id);
      let response = await this.$api.$get(`/items/${id}`, );
      this.items = []
      this.items.push(response)
    },
    async addToCart(){

    } 
  },
  async addToCart(item){
    this.cart.push(item) 
    console.log(this.cart);
  }
}
</script>
