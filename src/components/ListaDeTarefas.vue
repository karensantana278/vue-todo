<script setup>
  import {computed} from "vue";

  const props = defineProps(['tarefas', 'tarefasPendentes', 'tarefasFinalizadas', 'filtro'])

const temTarefasPendentes = computed(() => props.tarefasPendentes.length > 0)
const temTarefasFinalizadas = computed(() => props.tarefasFinalizadas.length > 0)
</script>

<template>
    <ul class="list-group mt-4">
        
      <li v-if="props.filtro == 'pendentes' && !temTarefasPendentes" class="list-group-item">
            Não existem tarefas pendentes
        </li>

        <li v-else-if="props.filtro == 'finalizadas' && !temTarefasFinalizadas" class="list-group-item">
            Não existem tarefas finalizadas
        </li>

        <li v-else  class="list-group-item" v-for="tarefa in props.tarefas">
          <input @change="evento => tarefa.finalizada = evento.target.checked" type="checkbox" :checked="tarefa.finalizada" :id="tarefa.titulo">
          <label :class="{ done : tarefa.finalizada }" class="ms-3" :for="tarefa.titulo">{{tarefa.titulo}}</label>
        </li>


      </ul>
</template>

<style scoped>

.done{
  text-decoration: line-through
}
</style>