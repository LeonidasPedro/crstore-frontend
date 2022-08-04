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
        to="/categories"
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
        name: null,
      },
      items:[],
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
        }
        await this.$axios.$post('http://localhost:3333/items/persist', item);
        this.$toast.success('Cadastro realizado com sucesso!');
        this.$router.push('/categories');
      } catch (error) {
        this.$toast.error('Ocorreu um erro ao realizar o cadastro!');
      }
    },
    async getCategories () {
      this.categories = await this.$axios.$get('http://localhost:3333/categories');
      console.log(this.categories.data);
    }

  }
}
</script>
