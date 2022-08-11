<template>
  <v-container>
    <v-container style="
        background-color:#d7d7d7
        border-radius: 1%;
        margin-top: 5%;">
    <v-form v-model="valid">   
      <v-container style="
          padding: 10%;">
          <h2
          style="
          text-align: center;
          color:#E53935;
          ">
            Cadastro
          </h2>
          
            <v-text-field 
              label="E-mail" 
              v-model="user.email"
              placeholder="Digite seu E-mail" 
              color="#ffb74d" 
              background-color="#d7d7d7"
              prepend-inner-icon="mdi-email"
              outlined />
            <v-text-field 
              label="Nome" 
              v-model="user.name"
              placeholder="Digite seu nome" 
              color="#ffb74d" 
              background-color="#d7d7d7"
              prepend-inner-icon="mdi-account"
              :rules="[rules.required]"
              outlined />
              <v-text-field 
              label="Telefone"
              v-model="user.phone"
              placeholder="Digite sua senha" 
              color="#ffb74d" 
              background-color="#d7d7d7"
              prepend-inner-icon="mdi-phone"
              :rules="[rules.required]"
              outlined />
            <v-text-field 
              label="Nome de Usuário" 
              v-model="user.username"
              placeholder="Digite seu nome de usuário" 
              color="#ffb74d"
              background-color="#d7d7d7"
              prepend-inner-icon="mdi-account-box" 
              :rules="[rules.required]"
              outlined />
            <v-text-field 
              label="Senha"
              v-model="user.password"
              type="password"
              placeholder="Digite sua senha" 
              color="#ffb74d" 
              background-color="#d7d7d7"
              prepend-inner-icon="mdi-lock"
              :rules="[rules.required]"
              outlined />
      </v-container>
    </v-form>
      <v-row>
        <v-btn 
        style="margin: auto;
        height: 50px;
        width: 330px;" 
        x-large color="#ffb74d" 
        @click="register"
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
            <a style="color:#E53935" 
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
  layout:'user',
  data () {
    return {
      user: {   
       cart:{},
       username:null, 
       name:null, 
       phone:'', 
       password:null, 
       role:'customer', 
       email:''
      },
      rules: {
          required: value => !!value || 'Campo Obrigatorio',
        },
      valid: false
    }
  },
   methods: {
    async register () {
      try {
        if (!this.valid){
          return this.$toast.warning('Preencha todos os campos corretamente!!');
        }
        console.log(JSON.stringify(this.user));
        let response = await this.$api.post(`/users/register`, this.user)
        if (response.type == 'success'){
          this.$toast.success(`Conta criada com sucesso`);
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

