<template>
  <ContainerDefault>
    <div class="d-flex justify-space-between">
      <h2>Produtos</h2>
      <v-btn
        color="secondary"
        prepend-icon="$plus"
        :to="{name: 'form-product'}"
      >
        Novo Produto
      </v-btn>
    </div>
    <v-data-table :headers="headers" :items="products">
      <template v-slot:item.actions="{ item }">
        <v-btn size="small" color="warning" @click="editProduct(item.id)">
          Editar
        </v-btn>
      </template>
    </v-data-table>
  </ContainerDefault>
</template>

<script setup>
import { useApi } from '@/composables/useApi';
import { useNotification } from '@/composables/useNotification';
import { useRouter } from 'vue-router';

const notification = useNotification()
const api = useApi()
const router = useRouter()

const headers = [
    { title: 'Name', value: 'name' },
    { title: 'Status', value: 'status' },
    { title: 'Ações', value: 'actions' },
  ]

const products = ref([])

async function getProducts(){
  try {
    const response = await api.get('/product')
    products.value = response.data
  } catch (error) {
    console.error(error)
    notification.error('Erro ao listar produtos')
  }
}

onMounted(() => {
  getProducts()
})

function editProduct(id){
  router.push({name: 'form-product', params: {id: id}})
}
</script>
