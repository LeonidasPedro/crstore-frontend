<template>
  <v-container>
    <h1>Produtos</h1>
    <hr>
    <v-container>
      <v-row>
        <v-col>
          <v-btn
            large
            color="primary"
            @click="getItems"
          >
            <v-icon style="margin-left: 5%">
              mdi-magnify
            </v-icon>
          </v-btn>
          <v-btn
            large
            color="success"
            to="/admin/items/itemsRegister"
          >
            Cadastrar
            <v-icon style="margin-left: 5%">
              mdi-plus-circle-outline
            </v-icon>
          </v-btn>
        </v-col>
      </v-row>
    </v-container>
    <v-container>
      <v-data-table
        :headers="headers"
        :items="items"
        :items-per-page="10"
        class="elevation-1"
      >
        <template v-slot:item.actions="{ item }">
          <v-icon
            small
            class="mr-2"
            @click="editItem(item)"
          >
            mdi-pencil
          </v-icon>
          <v-icon
            small
            @click="destroyItem(item)"
          >
            mdi-delete
          </v-icon>
        </template>
      </v-data-table>
    </v-container>
  </v-container>
</template>

<script>
export default {
  name: 'ItemsPage',
  layout:'admin',
  data () {
    return {
       headers: [
        {
          text: 'Produto', //nome da coluna
          align: 'center', //alinhamento -center, end, start
          sortable: false, //se permite ordenação dos dados por essa coluna
          value: 'name', //é o dado que essa coluna vai receber
        },
        {
          text: 'ID',
          align: 'center',
          sortable: false,
          value: 'id',
        },
        {
          text: 'Preço',
          align: 'center',
          sortable: false,
          value: 'price',
        },
        { text: "", value: "actions" }
      ],
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
      let response = await this.$api.get('/categories');
      this.categories = response.data
    },
    async getItems () {
      let response = await this.$api.get('/items');
      this.items = response.data
      
    },
    async destroyItem (item) {
      try {
        if (confirm(`Deseja deletar o registro id ${item.id} - ${item.name}?`)) {
          let response = await this.$api.post('/items/destroy', { id: item.id });
          this.$toast.success(response.message)
          this.getItems();
        }
      } catch (error) {
        this.$toast.error('Ocorreu um erro ao deletar o registro');
      }
    },
    async editItem(item){
      this.$router.push({
        name:'admin-items-itemsRegister',
        params:{ id: item.id}
      })
    }
  },

}
</script>
