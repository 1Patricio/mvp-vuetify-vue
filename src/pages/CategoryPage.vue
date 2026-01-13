<template>
  <ContainerDefault>
    <div class="d-flex justify-space-between">
      <h2>Categorias</h2>
      <v-btn color="secondary" prepend-icon="$plus">
        Nova Categoria
      </v-btn>
    </div>
    <v-data-table :items="categories"></v-data-table>
  </ContainerDefault>
</template>

<script setup>

const categories = [
  {
    name: "Produto 1",
    price: "5,45",
    description: "Descrição 1"
  },
  {
    name: "Produto 2",
    price: "5,45",
    description: "Descrição 2"
  },
  {
    name: "Produto 2",
    price: "5,45",
    description: "Descrição 2"
  },
  {
    name: "Produto 2",
    price: "5,45",
    description: "Descrição 2"
  },
  {
    name: "Produto 2",
    price: "5,45",
    description: "Descrição 2"
  },
  {
    name: "Produto 2",
    price: "5,45",
    description: "Descrição 2"
  },
  {
    name: "Produto 2",
    price: "5,45",
    description: "Descrição 2"
  },
  {
    name: "Produto 2",
    price: "5,45",
    description: "Descrição 2"
  },
  {
    name: "Produto 2",
    price: "5,45",
    description: "Descrição 2"
  },
  {
    name: "Produto 2",
    price: "5,45",
    description: "Descrição 2"
  },
  {
    name: "Produto 2",
    price: "5,45",
    description: "Descrição 2"
  },
  {
    name: "Produto 2",
    price: "5,45",
    description: "Descrição 2"
  },
  {
    name: "Produto 2",
    price: "5,45",
    description: "Descrição 2"
  },
  {
    name: "Produto 2",
    price: "5,45",
    description: "Descrição 2"
  },
  {
    name: "Produto 2",
    price: "5,45",
    description: "Descrição 2"
  },
  {
    name: "Produto 2",
    price: "5,45",
    description: "Descrição 2"
  },
  {
    name: "Produto 2",
    price: "5,45",
    description: "Descrição 2"
  },
  {
    name: "Produto 2",
    price: "5,45",
    description: "Descrição 2"
  },
  {
    name: "Produto 2",
    price: "5,45",
    description: "Descrição 2"
  },
  {
    name: "Produto 2",
    price: "5,45",
    description: "Descrição 2"
  },
]
</script>
