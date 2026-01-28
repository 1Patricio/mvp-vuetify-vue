<template>
  <v-layout>
    <v-app-bar color="secondary">
      <v-app-bar-nav-icon @click.stop="drawer = !drawer"></v-app-bar-nav-icon>

      <v-toolbar-title>
        Projeto Vuetify
      </v-toolbar-title>

      <v-btn icon="mdi-logout" @click="dialogLogout = true"></v-btn>
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
      <v-dialog
        v-model="dialogLogout"
        max-width="400"
      >
        <v-card
          prepend-icon="mdi-logout"
          title="Deseja encessar sua sessão?"
        >
          <template v-slot:actions>
            <v-spacer></v-spacer>

            <v-btn @click="handleLogout()">
              Sair
            </v-btn>
          </template>
        </v-card>
      </v-dialog>
    </v-main>
  </v-layout>
</template>

<script setup>
import { useRouter } from 'vue-router'

const router = useRouter()

const drawer = ref(true)
const dialogLogout = ref(false)

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

function handleLogout() {
  localStorage.removeItem('v-token')
  router.replace('/')
}
</script>
