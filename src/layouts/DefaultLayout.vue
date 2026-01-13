<template>
  <v-layout>
    <v-app-bar color="secondary">
      <v-app-bar-nav-icon @click.stop="drawer = !drawer"></v-app-bar-nav-icon>

      <v-toolbar-title>
        Projeto Vuetify
      </v-toolbar-title>
    </v-app-bar>

    <v-navigation-drawer v-model="drawer" :width="160">
      <v-list>
        <v-list-item
          v-for="menu in items"
          :key="menu.value"
          :title="menu.title"
          :value="menu.value"
          :to="{name: menu.value}"
        >

        </v-list-item>
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
    value: 'home'
  },
  {
    title: 'Categorias',
    value: 'category'
  },
  {
    title: 'Produtos',
    value: 'product'
  }
]
</script>
