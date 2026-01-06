<template>
  <v-layout>
    <v-app-bar color="yellow">
      <v-app-bar-nav-icon @click.stop="drawer = !drawer"></v-app-bar-nav-icon>

      <v-toolbar-title>
        Projeto Vuetify
      </v-toolbar-title>
    </v-app-bar>

    <v-navigation-drawer v-model="drawer" :width="160">
      <v-list :items="items">

      </v-list>
    </v-navigation-drawer>

    <v-main style="height: 100dvh;">
      <router-view />
    </v-main>
  </v-layout>
</template>

<script setup>
const drawer = ref(true)
const items = [
  {
    title: 'Dashboard',
    value: 'dashboard'
  },
  {
    title: 'Categorias',
    value: 'categorias'
  },
  {
    title: 'Produtos',
    value: 'produtos'
  }
]
</script>
