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
        to="/admin/categories"
      >
        Cancelar
      </v-btn>
    </v-container>
  </v-container>
</template>

<script>
export default {
  name: 'RegisterItemsPage',
  layout:'admin',
  data () {
    return {
      valid: false,
      item: {
        id:null,
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
          name: this.item.name
        }
         if(this.item.id === null){
          await this.$api.post('/categories/persist', item);
          this.$toast.success('Cadastro realizado com sucesso!');
          this.$router.push('/admin/categories');
        }
        await this.$api.post(`/categories/persist/${this.item.id}`, item);
        console.log(this.item.id);
          this.$toast.success('Cadastro realizado com sucesso!');
          this.$router.push('/admin/categories');
      } catch (error) {
        this.$toast.error('Ocorreu um erro ao realizar o cadastro!');
      }
    },
    async getCategories () {
      let response = await this.$api.get('/categories');
      this.items = response.data
    },
    async getById (id) {
      this.item = await this.$api.get(`/categories/${id}`);
    },
  }
}
</script>
