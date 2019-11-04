<template>
  <v-app>
    <v-app-bar color="white" flat app>
      <v-toolbar-title>
        <span class="headline font-weight-regular grey--text text--darken-3">
          #> PictHash
        </span>
      </v-toolbar-title>
    </v-app-bar>

    <v-content class="white">
      <router-view />
    </v-content>
  
    <v-footer color="white" app>
      <v-col class="text-left" cols="12">
        <span class="grey--text text--darken-1 body-2">&copy;{{ new Date().getFullYear() }} PictHash</span>
      </v-col>
    </v-footer>
  </v-app>
</template>

<script>
import Vue from 'vue';

export default Vue.extend({
  name: 'App',
  data: () => ({
    //
  }),
});
</script>
