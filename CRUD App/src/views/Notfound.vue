/** 
     Author:    Build Rise Shine with Nyros (BRS) 
     Created:   11.05.2022 
     Library / Component: NotFound Page

     (c) Copyright by BRS with Nyros. 
**/
<template>
    <div>
  <v-container>
    <v-card elevation="2" class="mx-auto"
    max-width="450">
        <h1>Oops!</h1>
        <h3>The {{ resource }} you're looking for is not here.</h3>
        <router-link :to="{ name: 'home' }">Back to the home page</router-link>
        </v-card>
  </v-container>
    </div>
</template>
<script>
export default {
  props: {
    resource: {
      type: String,
      required: true
    }
  }
}
</script>
