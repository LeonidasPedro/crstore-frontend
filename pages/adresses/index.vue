<template>
  <v-container>
    <v-container>
      <v-row>
        <v-col cols="12">
            <v-card
              class="mx-auto"
              max-width="300"
              tile
            >
              <v-list flat>
                <v-subheader>Endereços</v-subheader>
                <v-list-item-group
                  v-model="selectedItem"
                  color="orange lighten-2"
                >
                  <v-list-item
                    v-for="(item, i) in items"
                    :key="i"
                    @click="editItem(item.id)"
                  >
                    <v-list-item-content>
                      <p>{{item.adress}}, {{item.number}}, {{item.district}}, {{item.city}}</p>
                    </v-list-item-content>
                  </v-list-item>
                </v-list-item-group>
              </v-list>
            </v-card>
          </v-col>
      </v-row>
        <v-row justify="center">
           <v-btn
                rounded
                @click="
                adress = {};
                dialog= true"
                color="#E53935"
                dark
              >
                Novo Endereço
              </v-btn>
          <v-dialog
            v-model="dialog"
            persistent
            max-width="600px"
          >
            <v-card>
              <v-card-title>
                <span class="text-h5">Meu Endereço</span>
              </v-card-title>
              <v-card-text>
                <v-form v-model="valid">
                  <v-container>
                    <v-row>
                      <v-col
                        cols="12"
                        sm="6"
                        md="4"
                      >
                        <v-text-field
                          label="Bairro"
                          v-model="adress.district"
                        ></v-text-field>
                      </v-col>
                      <v-col cols="4">
                        <v-text-field
                          label="N° Residência"
                          v-model="adress.number"
                          required
                        ></v-text-field>
                      </v-col>
                       <v-col cols="3">
                        <v-text-field
                          label="UF"
                          v-model="adress.state"
                          required
                        ></v-text-field>
                      </v-col>
                      <v-col cols="12">
                        <v-text-field
                          label="Endereço"
                          v-model="adress.adress"
                          required
                        ></v-text-field>
                      </v-col>
                      <v-col
                        cols="12"
                        sm="6"
                      >
                      <v-text-field
                          label="Cep"
                          v-model="adress.cep"
                          required
                        ></v-text-field>
                      </v-col>
                      <v-col
                        cols="12"
                        sm="6"
                      >
                        <v-text-field
                          label="Cidade"
                          v-model="adress.city"
                          required
                        ></v-text-field>
                      </v-col>
                    </v-row>
                  </v-container>
                </v-form> 
              </v-card-text>
              <v-card-actions>
                <v-spacer></v-spacer>
                <v-btn
                  color="blue darken-1"
                  text
                  @click="destroy(item.id);
                  dialog=false"
                  style="color:red"
                >
                  Excluir
                </v-btn>
                <v-btn
                  color="blue darken-1"
                  text
                  @click="dialog = false"
                >
                  Cancelar
                </v-btn>
                <v-btn
                  color="blue darken-1"
                  text
                  @click="persist(item.id)"
                >
                  Salvar
                </v-btn>
              </v-card-actions>
            </v-card>
          </v-dialog>
        </v-row>
    </v-container>
  </v-container>
</template>

<script>
export default {
  layout:'user',
  name: 'AdressesPage',
  data () {
    return {
      item:{id:null},
      valid:null,
      dialog: false,
      items: [],
      selectedItem: 0,
      adress:{
        adress:null,
        number:null,
        district:null,
        cep:null,
        city:null,
        state:null
      }
    }
  },
  created () { //executado toda vez que a pagina é carregada
    this.getItems()
  },
  methods: {
    async getItems () {
      
        let response = await this.$api.get('/adresses');
        this.items = []
        this.items = response.data
      
    },
    async editItem(id){
      try {
        this.item.id = id
        let res = await this.$api.get(`/adresses/${id}`);
        this.dialog = true;
        this.adress = res
      } catch (error) {
        return this.$toast.error(`🤌🤌 Erro: ${error.message}`);
      }
    },
    async persist(id){
        try {
          this.dialog = false;
          if (!this.valid) {
            return this.$toast.warning('Preencha todos os campos obrigatórios')
          }
          let adress = {
            adress:this.adress.adress,
            number:this.adress.number,
            district:this.adress.district,
            cep:this.adress.cep,
            city:this.adress.city,
            state:this.adress.state
          };
          if(!id){
            let res = await this.$api.post('/adresses/persist/', adress)
            if(res.type != 'success'){
             this.getItems()
             return this.$toast.error(`🤌🤌 Erro: ${res.message}`); 
            }
            this.$toast.success(`👨‍🍳 Item Cadastrado com sucesso`)
            this.getItems()
          }
            let res = await this.$api.post(`/adresses/persist/${id}`,adress);
            this.item = {}
             if(res.type!= 'success'){
             return this.$toast.error(`🤌🤌 Erro: ${res.message}`); 
            }
            this.$toast.success(`👨‍🍳 Item Cadastrado com sucesso`)
            this.getItems()
        } catch (error) {
           return this.$toast.error(`🤌🤌 Erro: ${error.message}`);
        }
    },
    async destroy(id){
       let res = await this.$api.post('/adresses/destroy/', {id:id})
       if(res.type != 'success'){
            return this.$toast.error(`🤌🤌 Erro: ${res.message}`); 
          }
          this.$toast.success(`👨‍🍳 Item deletado com sucesso`)
          this.getItems()
    }
    
  }, 
}
</script>
