<template>
  <v-container>
    <v-row>
      <img
      style="
      width:200px;
      weight: 200px" 
      src="../../assets/white.png" alt="">
    </v-row>
    <v-row>
        <v-col
          cols="12"
          sm="6"
          md="3"
        >
          <v-text-field
            label="E-mail"
          ></v-text-field>
        </v-col>  
    </v-row>
    <v-row>
      <v-col
        cols="12"
        sm="6"
        md="3"
        >
          <v-text-field
            label="Name"
          ></v-text-field>
        </v-col>  
    </v-row>
    <v-row>
      <v-col
        cols="12"
        sm="6"
        md="3"
        >
          <v-text-field
            label="Userame"
          ></v-text-field>
      </v-col> 
    </v-row>
    <v-row>
      <v-col
        cols="12"
        sm="6"
        md="3"
        >
          <v-text-field
            label="Password"
          ></v-text-field>
      </v-col>
    </v-row>
  </v-container>

</template>

<script>
export default {
  name: 'RegisterPage'
}
</script>

<style>

</style>