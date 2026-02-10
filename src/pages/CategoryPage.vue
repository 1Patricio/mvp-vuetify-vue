<template>
  <ContainerDefault>
    <div class="d-flex justify-space-between">
      <h2>Categorias</h2>
      <v-btn
        color="#1E2761"
        prepend-icon="$plus"
        :to="{name: 'form-category'}"
      >
        Nova Categoria
      </v-btn>
    </div>
    <v-data-table :headers="headers" :items="categories" :loading="loading">
      <template v-slot:item.status="{ item }">
        <ChipStatus
          :status="item.status"
        />
      </template>

      <template v-slot:item.actions="{ item }">
        <v-btn size="small" color="warning" @click="editCategory(item.id)">
          Editar
        </v-btn>
      </template>
    </v-data-table>
  </ContainerDefault>
</template>

<script setup>
import ChipStatus from '@/components/ChipStatus.vue';
import { useNotification } from '@/composables/useNotification';
import { useCategoryService } from '@/services';
import { useRouter } from 'vue-router';

const notification = useNotification()
const router = useRouter()
const categoryService = useCategoryService()

const loading = ref(false)

const headers = [
    { title: 'Name', value: 'name' },
    { title: 'Status', value: 'status' },
    { title: 'Ações', value: 'actions' },
  ]

const categories = ref([])

async function getCategories(){
  loading.value = true
  try {
    categories.value = await categoryService.getAll()
  } catch (error) {
    console.error(error)
    notification.error('Erro ao listar categorias')
  } finally {
    loading.value = false
  }
}

onMounted(() => {
  getCategories()
})

function editCategory(id){
  router.push({name: 'form-category', params: {id: id}})
}
</script>
