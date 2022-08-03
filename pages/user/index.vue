<template>
 <v-container
  style="margin-left: 30%">
  <img
  src="../../assets/white.png" alt="">
  <v-row>
  <v-col>
    <v-btn
    to="/user/register"
    elevation="2"
    style="width: 200px;
    margin-left: -10%;"
    >Register</v-btn>
  </v-col>
  <v-col>
    <v-btn
    style="
    margin-left: -65%;
    width: 200px"
    to="/user/login"
    elevation="2"
    >login</v-btn>
  </v-col>
  </v-row>
  
 </v-container>
</template>

<script>
export default {
  name: 'IndexPage'
}
</script>
