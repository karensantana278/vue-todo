<script setup>

import { reactive } from 'vue';

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
    <header class="p-5 mb-4 mt-4 text-center">
      <h1>Minhas tarefas</h1>
      <p>Você possui {{getTarefasPendentes().length}} tarefas pendentes</p>
    </header>

    <main class="p-5 bg-light rounded-3">
      <form @submit.prevent="cadastraTarefa">
        <div class="row">

          <div class="mb-3 col-12 col-md-8 ">
            <div class="input-group">
            <input :value="estado.tarefaTemporaria" @change="evento => estado.tarefaTemporaria = evento.target.value" required class="form-control" type="text" placeholder="Adicione uma tarefa">
            <button class="btn btn-primary" type="submit">Cadastrar</button>
          </div>
          </div>
          
          <div class="col-md-4">
            <select @change="evento => estado.filtro = evento.target.value" class="form-select">
              <option value="todas">Todas tarefas</option>
              <option value="pendentes">Pendentes</option>
              <option value="finalizadas">Finalizadas</option>
            </select>
          </div>

        </div>
      </form>
      
      <ul class="list-group mt-4">
        <li class="list-group-item" v-for="tarefa in getTarefasFiltradas()">
          <input @change="evento => tarefa.finalizada = evento.target.checked" type="checkbox" :checked="tarefa.finalizada" :id="tarefa.titulo">
          <label :class="{ done : tarefa.finalizada }" class="ms-3" :for="tarefa.titulo">{{tarefa.titulo}}</label>
        </li>
      </ul>

    </main>

  </div>
  
</template>

<style scoped>

.done{
  text-decoration: line-through
}
</style>
