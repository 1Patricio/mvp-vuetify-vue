<template>
    <ContainerDefault>
    <div class="d-flex justify-space-between">
      <h2>Cadastro de Categoria</h2>
    </div>

      <v-form class="mt-3" v-model="valid" @submit.prevent="handleSubmit()">
        <v-text-field
          v-model="formCategory.name"
          label="Nome"
          required
          variant="outlined"
          type="text"
          class="mb-1"
          :rules="[rules.required]"
        ></v-text-field>

        <v-select
          v-model="formCategory.status"
          label="Status"
          :items="status"
          item-title="title"
          item-value="value"
          persistent-hint
          single-line
          variant="outlined"
          :rules="[rules.required]"
        ></v-select>

        <div class="d-flex justify-end ga-2">
          <v-btn :to="{name: 'category'}">
            Voltar
          </v-btn>

          <v-btn
            color="#1E2761"
            type="submit"
            :disabled="!valid"
          >
            {{idCategory ? 'Atualizar' : 'Cadastrar'}}
          </v-btn>
        </div>
      </v-form>
  </ContainerDefault>
</template>

<script setup>
import { useNotification } from '@/composables/useNotification'
import { onMounted } from 'vue'
import { useRoute, useRouter } from 'vue-router'
import { useCategoryService } from '@/services';

const notification = useNotification()
const router = useRouter()
const route = useRoute()
const categoryService = useCategoryService()

const idCategory = ref('')
const valid = ref(false)

const formCategory = ref({
  name: '',
  status: 'active'
})

const status = [
  { title: 'Ativo', value: 'active'},
  { title: 'Inativo', value: 'inactive'}
]

const rules = {
  required: value => !!value || 'Campo obrigatório'
}

onMounted(() => {
  if (route.params?.id) {
    idCategory.value = route.params?.id
    getCategory(idCategory.value)
  }
})

function handleSubmit() {
  if(!valid.value) {
    notification.error('Formulário incompleto')
  }
  idCategory.value ? updateCategory(idCategory.value) : createCategory()
}

async function createCategory(){
  try {
    await categoryService.create(formCategory.value)
    notification.success('Categoria cadastrada com sucesso')
    router.push({ name: 'category' })
  } catch (error) {
    console.error(error)
    notification.error('Erro ao salvar categoria')
  }
}

async function getCategory(id) {
  try {
    const data = await categoryService.getById(id)
    formCategory.value = {
      name: data.name,
      status: data.status
    }
  } catch (error) {
    console.error(error)
    notification.error('Erro ao buscar categoria')
  }
}

async function updateCategory(id){
  try {
    categoryService.update(id, formCategory.value)

    notification.success('Categoria atualizada com sucesso')
    router.push({ name: 'category' })
  } catch (error) {
    console.error(error)
    notification.error('Erro ao salvar categoria')
  }
}
</script>
