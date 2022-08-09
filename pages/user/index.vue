<template>
  <v-container
        style="
        height: 430px;
        width: 460px;
        background-color: #202024;
        border-radius: 1%;
        margin-bottom:10%"
        >
          <v-container
          style="
          padding: 10%;">

            <v-form v-model="valid">
                <v-text-field
                      label="Usuário"
                      v-model="user.username"
                      placeholder="Digite seu Nome de Usuário"
                      color="#ffb74d"
                      prepend-inner-icon="mdi-email"
                      outlined
                    />
                  <v-text-field
                    label="Senha"
                    v-model="user.password"
                    placeholder="Digite sua senha"
                    color="#ffb74d"
                    prepend-inner-icon="mdi-lock"
                    outlined
                  />
              </v-form>

              <v-container
              style="
              margin-top: -39px;
              margin-left: -10px;
              margin-bottom: -30px;">
                <a
                style="color:#ffb74d"
                href="https://www.youtube.com/watch?v=dQw4w9WgXcQ">Esqueci minha senha</a>
              </v-container>
            </v-container>
    <v-row>
       <v-btn
        style="margin: auto;
        height: 50px;
        width: 330px;"
        x-large
        @click="login"
        color="#ffb74d"
        dark
        
        >
        Entrar
        </v-btn>
    </v-row>
    <br>
    <v-row>
     <v-container
     style="
     text-align:center"
     >
        <p>
          Não tem uma conta?
          <a
          style="color:#ffb74d"
          href="/user/register">Registre-se
          </a>
        </p>
     </v-container>
    </v-row>
  </v-container>
</template>

<script>
export default {
  name:"loginPage",
  layout:"user",
  data () {
    return {
      user: {   
        username: null,
        password: "",
      },
      rules: {
          required: value => !!value || 'Field required',
        },
      valid: false
    }
  },
  methods: {
    async login () {
        if (!this.valid){
          return this.$toast.warning('Preencha todos os campos corretamente!!');
        }
          console.log(JSON.stringify(this.user));

          let response = await this.$api.$post(`/users/login`, this.user)

        if (response.type == 'success'){
          localStorage.removeItem('crstore-api-token')
          localStorage.setItem('crstore-api-token', response.token)
          this.$toast.success(`Login feito com sucesso!`);
          return this.$router.push('/');
        }
        else {
          return this.$toast.warning(`${response.message}`);
        }
    }
  }
}
</script>

