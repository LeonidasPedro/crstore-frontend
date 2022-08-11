<template>
   <v-container>
        <v-row>
          <v-col cols="2">
            <v-card
              class="mx-auto"
              max-width="300"
              tile
            >
              <v-list flat>
                <v-subheader
                >Categorias</v-subheader>
                <v-list-item-group
                  v-model="selectedItem"
                  color="orange lighten 2"
                >
                  <v-list-item
                    v-for="(categorie, i) in categories"
                    :key="i"
                    @click="getByCategory(categorie)"
                  >
                    <v-list-item-content>
                      <v-list-item-title v-text="categorie.name"></v-list-item-title>
                    </v-list-item-content>
                  </v-list-item>
                </v-list-item-group>
              </v-list>
            </v-card>
          </v-col>
          <v-col>
            <v-sheet
              min-height="70vh"
              rounded="lg"
             
              color="transparent"
             
            >
              <v-container>
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
                          color="red darken-1"
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
            </v-sheet>
          </v-col>
        </v-row>
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
      let response = await this.$api.get('/categories');
      this.categories = response.data
    },
    async getItems () {
      let response = await this.$api.get('/items');
      this.items = response.data
    },
    async getByCategory(categorie){
      console.log(categorie);
      let id = {
        idCategory:categorie.id
      }
      let response = await this.$api.post(`/items/category/`, id);
      this.items = response.data
    },
    async getById(){
      let id = this.item.id
      console.log(id);
      let response = await this.$api.get(`/items/${id}`, );
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
