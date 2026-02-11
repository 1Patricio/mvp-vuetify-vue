<template>
  <ContainerDefault>
    <div class="d-flex mb-1 justify-space-between">
      <h2>Dashboard</h2>
    </div>
    <v-row>
      <v-col cols="12" sm="4">
        <CardDashboard
          card-title="Categorias"
          :card-value="categoriesTotal"
          card-icon="mdi-shape-outline"
        />
      </v-col>
      <v-col cols="12" sm="4">
        <CardDashboard
          card-title="Produtos"
          :card-value="productsTotal"
          card-icon="mdi-package-variant"
        />
      </v-col>
    </v-row>
  </ContainerDefault>
</template>

<script setup>
import { useNotification } from '@/composables/useNotification';
import { useCategoryService, useProductService } from '@/services';
import { onMounted } from 'vue';

const categoryService = useCategoryService()
const productService = useProductService()
const notification = useNotification()

const loading = ref(false)
const categoriesTotal = ref(0)
const productsTotal = ref(0)

async function getCategoriesTotal () {
  loading.value = true
  try {
    categoriesTotal.value = await categoryService.getTotal()
  } catch (error) {
    notification.error('Não foi possível recuperar as categorias', error)
  } finally {
    loading.value = false
  }
}

async function getProductsTotal () {
  loading.value = true
  try {
    productsTotal.value = await productService.getTotal()
  } catch (error) {
    notification.error('Não foi possível recuperar os produtos', error)
  } finally {
    loading.value = false
  }
}

onMounted(() => {
  getCategoriesTotal()
  getProductsTotal()
})
</script>
