<template>
  <v-select
    v-model="model"
    label="Categorias"
    :items="categories"
    item-title="name"
    item-value="id"
    persistent-hint
    variant="outlined"
    :rules="props.rules"
    :loading="loading.value"
  ></v-select>
</template>

<script setup>
import { useNotification } from '@/composables/useNotification'
import { useCategoryService } from '@/services'

const notification = useNotification()
const categoryService = useCategoryService()

const props = defineProps({
  rules: {
    type: Array,
    default: () => []
  }
})

const model = defineModel({ required: true})

const categories = ref([])
const loading = ref(false)

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
</script>
