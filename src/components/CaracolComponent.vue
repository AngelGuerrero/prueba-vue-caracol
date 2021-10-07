<script setup>
import { ref, onMounted } from 'vue'
import ListComponent from './ListComponent.vue';

const m = () => ([
  [1, 2, 3],
  [4, 5, 6],
  [7, 8, 9]
])

const m2 = () => ([
  [1, 2, 3, 4],
  [5, 6, 7, 8],
  [9, 10, 11, 12]
])

const r = ref([])
const r2 = ref([])

/**
 * El funcionamiento básico consiste en ir sacando
 * los elementos en dirección a las manecillas del reloj,
 * identificando la cabeza, la cola y el cuerpo de la lista.
 * 
 * @param {number[]} list - Lista de elementos a recorrer.
 * @param {number[]} [retval] - Acumulador, o lista de valores iniciales.
 * @return {number[]} - Devuelve los elementos de la lista ordenados en dirección de las manecillas del reloj.
 */
const caracol = (list, retval = []) => {
  list.forEach((_, idx) => {
    const isHead = idx === 0
    const isTail = idx === list.length - 1

    if (isHead) {
      const head = list.shift()
      retval.push(head)
    }

    if (!isTail) {
      if (!list[idx]) return retval

      const last = list[idx].pop()
      retval.push(last)
    }

    if (isTail) {
      if (!list[idx]) return retval

      const tail = list.pop()
      retval.push(tail.reverse())
    }
  });

  if (list.length >= 1) caracol(list, retval)

  return retval.flat()
}

onMounted(() => {
  r.value = caracol(Array.from(m()))

  r2.value = caracol(Array.from(m2()))
})

</script>

<template>
  <ListComponent :list="m()" title="Matriz de 'm'" :res="r" />
  <ListComponent :list="m2()" title="Matriz de 'm2'" :res="r2" />
</template>
