<template>
  <ContainerDefault>
    <div class="d-flex justify-space-between">
      <h2>Produtos</h2>
      <v-btn
        color="#1E2761"
        prepend-icon="$plus"
        :to="{name: 'form-product'}"
      >
        Novo Produto
      </v-btn>
    </div>
    <v-data-table :headers="headers" :items="products" :loading="loading">
      <template v-slot:item.status="{ item }">
        <ChipStatus
          :status="item.status"
        />
      </template>

      <template v-slot:item.actions="{ item }">
        <v-btn size="small" color="warning" @click="editProduct(item.id)">
          Editar
        </v-btn>
      </template>
    </v-data-table>
  </ContainerDefault>
</template>

<script setup>
import { useNotification } from '@/composables/useNotification';
import { useProductService } from '@/services';
import { useRouter } from 'vue-router';

const notification = useNotification()
const productService = useProductService()
const router = useRouter()

const headers = [
    { title: 'Name', value: 'name' },
    { title: 'Status', value: 'status' },
    { title: 'Ações', value: 'actions' },
  ]

const products = ref([])
const loading = ref(false)

async function getProducts(){
  loading.value = true
  try {
    products.value = await productService.getAll()
  } catch (error) {
    console.error(error)
    notification.error('Erro ao listar produtos')
  } finally {
    loading.value = false
  }
}

onMounted(() => {
  getProducts()
})

function editProduct(id){
  router.push({name: 'form-product', params: {id: id}})
}
</script>
