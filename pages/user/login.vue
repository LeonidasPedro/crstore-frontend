<template>
  <v-container>
    <v-row>
      <v-col>
        <img src="../../assets/white.png" alt="abubleble">
      </v-col>
      <v-col>
        <v-row>
          <v-col
          cols="10"
           >
          <v-text-field
            label="Username"
            >
          </v-text-field>
          </v-col>  
        </v-row>
        <v-row>
          <v-col
          cols="10"
           >
          <v-text-field
            label="Senha"
            >
          </v-text-field>
          </v-col>  
        </v-row>
        <v-row>
          <v-btn>
            Login
          </v-btn>
        </v-row>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  name: 'LoginUserPage'
}
</script>

<style>

</style>