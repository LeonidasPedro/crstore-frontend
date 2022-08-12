<template>
  <v-container>
    <h1>Cadastrar Itens</h1>
    <hr>
    <v-form v-model="valid">
      <v-container>
        <v-row>
          <v-col>
            <v-text-field
              v-model="item.name"
              placeholder="Nome"
              label="Nome"
              required
              :rules="rule"
              outlined
            />
          </v-col>
           <v-col
            cols="3">
            <v-text-field
              v-model="item.price"
              placeholder="Valor"
              label="Valor"
              required
              :rules="rule"
              outlined
            />
          </v-col>
        </v-row>
        <v-row>
          <v-col
            cols="3"
          >
            <v-autocomplete
              v-model="item.idCategory"
              :items="categories.data"
              outlined
              label="Categoria"
              item-text="name"
              item-value="id"
              required
              :rules="rule"
            ></v-autocomplete>
          </v-col>
           <v-col
            cols="9"
          >
            <v-text-field
              v-model="item.thumbnail"
              placeholder="Link da Imagem"
              label="Link da Imagem"
              outlined
            />
          </v-col>
        </v-row>
        <v-row>
          <v-textarea
            v-model="item.description"
            clearable
            clear-icon="mdi-close-circle"
            label="Descrição"
            value="Descrição do item"
          ></v-textarea>
        </v-row>
      </v-container>
    </v-form>
    <v-container>
      <v-btn
        color="success"
        style="float: right;"
        large
        @click="persist"
      >
        Salvar
      </v-btn>
      <v-btn
        color="error"
        large
        to="/admin/items"
      >
        Cancelar
      </v-btn>
    </v-container>
  </v-container>
</template>

<script>
export default {
  name: 'RegisterItemsPage',
  layout: 'admin',
  data () {
    return {
      valid: false,
      item: {
        id: null,
        name: null,
        price: null,
        idCategory: null,
        thumbnail:null,
        description:null
      },
      categories: [],
      rule: [
        v => !!v || 'Esse campo é obrigatório'
      ]
    }
  },
  created () {
    if(this.$route?.params?.id){
      this.getById(this.$route.params.id)
    }
    this.getCategories();
  },
  methods: {
    async persist () {
      try {
        if (!this.valid) {
          return this.$toast.warning('Preencha todos os campos obrigatórios')
        }
        let item = {
          name: this.item.name,
          price: this.item.price,
          idCategory: this.item.idCategory,
          thumbnail: this.item.thumbnail,
          description: this.item.description
        }
        
        if(this.item.id === null){
          let res = await this.$api.post('/items/persist', item);
          if(res.type == 'error'){
            return this.$toast.error(`🤌🤌 Erro: ${res.message}`); 
          }
          this.$toast.success(`👨‍🍳 ${res.message}`)
          this.$router.push('/admin/items');
        }
        let res = await this.$api.post(`/items/persist/${this.item.id}`, item);
           if(res.type == 'error'){
             return this.$toast.error(`🤌🤌 Erro: ${res.message}`); 
            }
          this.$toast.success(`👨‍🍳 ${res.message}`)
          this.$router.push('/admin/items');
        
      } catch (error) {
         return this.$toast.error(`🤌🤌 Erro: ${error.message}`);
      }
    },

    async getCategories () {
      this.categories = await this.$api.get('/categories');
      console.log(this.categories.data);
    },
     async getById (id) {
      this.item = await this.$api.get(`/items/${id}`);
      console.log(this.item.id);
    },

  }
}
</script>
