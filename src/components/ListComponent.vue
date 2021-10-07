<script setup>
/**
 * ListComponent.
 * 
 * Componente creado únicamente para mostrar los resultados obtenidos del algoritmo.
 */
defineProps({
  list: {
    type: Array,
    required: true
  },

  title: {
    type: String,
    required: true,
  },

  res: {
    type: Array,
    required: true
  }
})
</script>

<template>
  <h1>{{ title }}</h1>

  <div class="container">
    <div class="item" v-for="(item, idx) in list" :key="idx">
      <div class="item__number" v-for="n in item" :key="n.id">{{ n }}</div>
    </div>
  </div>

  <h3>Respuesta</h3>
  <div class="response">{{ res }}</div>
</template>

<style scoped>
.container {
  width: 50%;
  max-width: 300px;
}

.item {
  display: flex;
}

.item__number {
  border: 1px solid #ccc;
  width: 5rem;
  height: 5rem;

  display: flex;
  justify-content: center;
  align-items: center;
  flex-grow: 1;
}

.response {
  background-color: rgb(37, 36, 36);
  color: white;
  padding: 1rem;
  border-radius: 0.5rem;
  margin: 1rem 0;
  width: 50%;
  max-width: 300px;
}
</style>
