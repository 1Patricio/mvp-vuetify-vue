<template>
    <ContainerDefault>
    <div class="d-flex justify-space-between">
      <h2>Cadastro de Produtos</h2>
    </div>

      <v-form class="mt-3" v-model="valid" @submit.prevent="handleSubmit()">
        <v-text-field
          v-model="formProduct.name"
          label="Nome"
          required
          variant="outlined"
          type="text"
          class="mb-1"
          :rules="[rules.required]"
        ></v-text-field>

        <v-textarea
          v-model="formProduct.description"
          label="Descrição"
          variant="outlined"
          class="mb-1"
          :rules="[rules.required]"
        ></v-textarea>

        <v-text-field
          v-model="formProduct.price"
          label="Preço"
          variant="outlined"
          type="number"
          class="mb-1"
          :rules="[rules.required]"
        ></v-text-field>

        <v-select
          v-model="formProduct.status"
          label="Status"
          :items="status"
          item-title="title"
          item-value="value"
          persistent-hint
          single-line
          variant="outlined"
          :rules="[rules.required]"
        ></v-select>

        <SelectCategory v-model="formProduct.category_id" :rules="[rules.required]" />

        <div class="d-flex justify-end ga-2">
          <v-btn :to="{name: 'product'}">
            Voltar
          </v-btn>

          <v-btn
            color="secondary"
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
import SelectCategory from '@/components/SelectCategory.vue'
import { useApi } from '@/composables/useApi'
import { useNotification } from '@/composables/useNotification'
import { onMounted } from 'vue'
import { useRoute, useRouter } from 'vue-router'

const notification = useNotification()
const api = useApi()
const router = useRouter()
const route = useRoute()
const idProduct = ref('')

const valid = ref(false)

const formProduct = ref({
  name: '',
  description: '',
  price: 0,
  status: 'active',
  category_id: null
})

const status = [
  { title: 'Ativo', value: 'active'},
  { title: 'Inativo', value: 'inactive'}
]

const rules = {
  required: value => !!value || 'Campo obrigatório',
}

onMounted(() => {
  if (route.params?.id) {
    idProduct.value = route.params?.id
    getProduct(idProduct.value)
  }
})

function handleSubmit() {
  if(!valid.value) {
    notification.error('Formulário incompleto')
  }
  idProduct.value ? updateProduct(idProduct.value) : createProduct()
}

async function createProduct(){
  try {
    await api.post('/product',{
      ...formProduct.value
    })
    notification.success('Produto cadastrado com sucesso')
    router.push({ name: 'category' })
  } catch (error) {
    console.error(error)
    notification.error('Erro ao salvar produto')
  }
}

async function getProduct(id) {
  try {
    const response = await api.get(`/product/${id}`)
    formProduct.value = {
      name: response.data.name,
      description: response.data.description,
      price: response.data.price,
      status: response.data.status,
      category_id: response.data.category_id
    }
  } catch (error) {
    console.error(error)
    notification.error('Erro ao buscar produto')
  }
}

async function updateProduct(id){
  try {
    await api.put(`/product/${id}`,{
      ...formProduct.value
    })
    notification.success('Produto atualizado com sucesso')
    router.push({ name: 'product' })
  } catch (error) {
    console.error(error)
    notification.error('Erro ao salvar produto')
  }
}
</script>
