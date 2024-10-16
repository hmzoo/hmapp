<template>
  <v-app>

    
      <v-app-bar app>
        <v-toolbar-title>HMAPP</v-toolbar-title>
        <v-spacer></v-spacer>
        <v-btn text to="/">Home</v-btn>
        <v-btn text to="/utils">Utils</v-btn>
  
      </v-app-bar>

    <v-main>
      <router-view />
    </v-main>

    <v-footer height="20" app>
        <div class="text-caption text-disabled" style="position: absolute; right: 16px;">
        </div>
      </v-footer>

  </v-app>
</template>

<script setup>
  //
</script>
