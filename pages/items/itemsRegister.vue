<template>
  <v-container>
    <h1>Items</h1>
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
            cols="4"
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
        to="/items"
      >
        Cancelar
      </v-btn>
    </v-container>
  </v-container>
</template>

<script>
export default {
  name: 'RegisterItemsPage',
  data () {
    return {
      valid: false,
      item: {
        id: null,
        name: null,
        price: null,
        idCategory: null
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
        }
        
        if(this.item.id === null){
          await this.$axios.$post('http://localhost:3333/items/persist', item);
          this.$toast.success('Cadastro realizado com sucesso!');
          this.$router.push('/items');
        }
        await this.$axios.$post(`http://localhost:3333/items/persist/${this.item.id}`, item);
          this.$toast.success('Cadastro realizado com sucesso!');
          this.$router.push('/items');
        
      } catch (error) {
        this.$toast.error('Ocorreu um erro ao realizar o cadastro!');
      }
    },

    async getCategories () {
      this.categories = await this.$axios.$get('http://localhost:3333/categories');
      console.log(this.categories.data);
    },
     async getById (id) {
      this.item = await this.$axios.$get(`http://localhost:3333/items/${id}`);
      console.log(this.item.id);
    },

  }
}
</script>
