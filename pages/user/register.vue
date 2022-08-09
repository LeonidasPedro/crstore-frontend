<template>
  <v-container>
    <v-container style="
        background-color: #202024;
        border-radius: 1%;
        margin-top: 5%;">
      <v-container style="
          padding: 10%;">
        <v-text-field 
          label="E-mail" 
          v-model="user.email"
          placeholder="Digite seu E-mail" 
          color="#ffb74d" 
          prepend-inner-icon="mdi-email"
          outlined />
        <v-text-field 
          label="Nome" 
          v-model="user.name"
          placeholder="Digite seu nome" 
          color="#ffb74d" 
          prepend-inner-icon="mdi-account"
          outlined />
        <v-text-field 
          label="Nome de Usuário" 
          v-model="user.username"
          placeholder="Digite seu nome de usuário" 
          color="#ffb74d"
          prepend-inner-icon="mdi-account-box" 
          outlined />
        <v-text-field 
          label="Senha"
          placeholder="Digite sua senha" 
          color="#ffb74d" 
          prepend-inner-icon="mdi-lock"
          outlined />
         <v-text-field 
          label="Confirmação de senha" 
          v-model="user.password"
          placeholder="Confirme sua senha" 
          color="#ffb74d" 
          prepend-inner-icon="mdi-lock"
          outlined />
      </v-container>
      <v-row>
        <v-btn 
        style="margin: auto;
       height: 50px;
       width: 330px;" 
       x-large color="#ffb74d" 
       dark>
        Cadastrar
        </v-btn>
      </v-row>
      <br>
      <v-row>
        <v-container 
        style="
        text-align:center">
          <p>
            Já tem uma conta?
            <a style="color:#ffb74d" 
            href="/user/">Página de Login
            </a>
          </p>
        </v-container>
      </v-row>
    </v-container>

  </v-container>

</template>

<script>
export default {
  data () {
    return {
      user: {   
       cart:{},
       username:null, name:null, phone:null, password:null, role:null, email:null
      },
      rules: {
          required: value => !!value || 'Campo Obrigatorio',
          min: v => v.length >= 8 || 'Deve conter no mínimo 8 caracteres',
        },
      valid: false
    }
  },
  methods: {
    async register () {
      try {
        if (!this.valid){
          return this.$toast.warning('Preencha todos os campos necessários');
        }
        console.log(JSON.stringify(this.user));
        let response = await this.$api.$post(`/users/register`, this.user)
        if (response.type == 'success'){
          this.$toast.success(`Usuário criado com sucesso!!`);
          return this.$router.push('/');
        }
        else {
          return this.$toast.warning(`${response.message}`);
        }
      } catch (error) {
        return this.$toast.error(`${error.message}`);
      }
    }
  }
}
</script>

<style>
</style>

