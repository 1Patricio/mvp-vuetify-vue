<template>
  <ContainerDefault>
    <div class="d-flex justify-space-between">
      <h2>Categorias</h2>
      <v-btn
        color="secondary"
        prepend-icon="$plus"
        :to="{name: 'form-category'}"
      >
        Nova Categoria
      </v-btn>
    </div>
    <v-data-table :headers="headers" :items="categories">
      <template v-slot:item.actions="{ item }">
        <v-btn size="small" color="warning" @click="editCategory(item.id)">
          Editar
        </v-btn>
      </template>
    </v-data-table>
  </ContainerDefault>
</template>

<script setup>
import { useApi } from '@/composables/useApi';
import { useAuth } from '@/composables/useAuth';
import { useNotification } from '@/composables/useNotification';
import { useRouter } from 'vue-router';

const notification = useNotification()
const api = useApi()
const router = useRouter()
const auth = useAuth()

const headers = [
    { title: 'Name', value: 'name' },
    { title: 'Status', value: 'status' },
    { title: 'Ações', value: 'actions' },
  ]

const categories = ref([])

async function getCategories(){
  try {
    const response = await api.get('/category')
    categories.value = response.data
  } catch (error) {
    console.error(error)
    notification.error('Erro ao listar categorias')
  }
}

onMounted(() => {
  getCategories()
})

function editCategory(id){
  router.push({name: 'form-category', params: {id: id}})
}
</script>
