<template>
  <v-container
        style="
        height: 430px;
        width: 460px;
        background-color: #202024;
        border-radius: 1%;
        margin-top: 5%;"
        >
          <v-container
          style="
          padding: 10%;">
            <v-text-field
                  label="E-mail"
                  placeholder="Digite seu E-mail"
                  color="#ffb74d"
                  prepend-inner-icon="mdi-email"
                  outlined
                />
                <v-text-field
                  label="Senha"
                  placeholder="Digite sua senha"
                  color="#ffb74d"
                  prepend-inner-icon="mdi-lock"
                  outlined
                />
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
  name: 'LoginUser'
}
</script>