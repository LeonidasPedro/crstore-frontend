<template>
  <v-container>
    <h1>Categorias</h1>
    <hr>
    <v-container>
      <v-row>
        <v-col>
          <v-btn
            large
            color="success"
            to="/admin/categories/registerCategories"
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
  layout: 'admin',
  data () {
    return {
      headers: [
        {
          text: 'Código', //nome da coluna
          align: 'center', //alinhamento -center, end, start
          sortable: false, //se permite ordenação dos dados por essa coluna
          value: 'id', //é o dado que essa coluna vai receber
        },
        {
          text: 'Nome',
          align: 'center',
          sortable: false,
          value: 'name',
        },
        { text: "", value: "actions" }
      ],
      items: []
    }
  },
  created () { //executado toda vez que a pagina é carregada
    this.getItems()
  },
  methods: {
    async getItems () {
      let response = await this.$axios.$get('http://localhost:3333/categories', { headers: { Authorization: `Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VySWQiOjEsInVzZXJuYW1lIjoiYWRtaW4iLCJpYXQiOjE2NTk2MzQxMzgsImV4cCI6MTY1OTY2MjkzOH0.8wYxBt7B-TstNT44DVkC5rGAj18JAsh0hodvyC7csmU` }});
      this.items = response.data
    },
    async destroyItem (item) {
      try {
        if (confirm(`Deseja deletar o registro id ${item.id} - ${item.titulo}?`)) {
          let response = await this.$axios.$post('http://localhost:3333/categories/destroy', { id: item.id });
          this.$toast.success(response.message)
          this.getItems();
        }
      } catch (error) {
        this.$toast.error('Ocorreu um erro ao deletar o registro');
      }
    },
    async editItem(item){
      this.$router.push({
        name:'admin-categories-registerCategories',
        params:{ id: item.id}
      })
    }
  }
}
</script>
