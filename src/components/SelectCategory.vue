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
  ></v-select>
</template>

<script setup>
import { useApi } from '@/composables/useApi'
import { useNotification } from '@/composables/useNotification'

const notification = useNotification()
const api = useApi()

const props = defineProps({
  rules: {
    type: Array,
    default: () => []
  }
})

const model = defineModel({ required: true})

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
</script>
