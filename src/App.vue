<script setup>

import { reactive } from 'vue';
import Cabecalho from './components/Cabecalho.vue'
import Formulario from './components/Formulario.vue'
import ListaDeTarefas from './components/ListaDeTarefas.vue'

const estado = reactive({
  tarefaTemporaria: '',
  filtro: "todas",
  tarefas:[
    {
      titulo: "Estudar ES6",
      finalizada: false,
    },
    {
      titulo: "Estudar Angular",
      finalizada: true,
    },
    {
      titulo: "Estudar testes",
      finalizada: false
    }
  ]
})

const getTarefasPendentes = () => {
  return estado.tarefas.filter( estado => !estado.finalizada )
}

const getTarefasFinalizadas = () => {
  return estado.tarefas.filter( estado => estado.finalizada )
}

const getTarefasFiltradas = () => {
  const {filtro} = estado

  switch(filtro){
    case 'pendentes':
      return getTarefasPendentes();
    case 'finalizadas': 
      return getTarefasFinalizadas();
    default:
      return estado.tarefas  
  }
}

const cadastraTarefa = () => {
  const tarefaNova = {
    titulo: estado.tarefaTemporaria,
    finalizada: false
  }

  estado.tarefas.push(tarefaNova)
  estado.tarefaTemporaria = '';
}


</script>

<template>
  <div class="container ">
  
    <Cabecalho :tarefas-pendentes="getTarefasPendentes().length" />

    <main class="p-5 bg-light rounded-3">

    <Formulario :trocar-filtro="evento => estado.filtro = evento.target.value" :tarefa-temporaria="estado.tarefaTemporaria" :edita-tarefa-temp="evento => estado.tarefaTemporaria = evento.target.value" :cadastra-tarefa="cadastraTarefa" />
    

      <ListaDeTarefas :filtro="estado.filtro" :tarefas="getTarefasFiltradas()" :tarefas-pendentes="getTarefasPendentes()" :tarefas-finalizadas="getTarefasFinalizadas()"/>

    </main>

  </div>
  
</template>


