<script setup>
    const props = defineProps(['cadastraTarefa', 'tarefaTemporaria', 'trocarFiltro', 'editaTarefaTemp'])
</script>

<template>
    <form @submit.prevent="props.cadastraTarefa">
        <div class="row">

          <div class="mb-3 col-12 col-md-8 ">
            <div class="input-group">
            <input :value="props.tarefaTemporaria" @change="props.editaTarefaTemp" required class="form-control" type="text" placeholder="Adicione uma tarefa">
            <button class="btn btn-primary" type="submit">Cadastrar</button>
          </div>
          </div>
          
          <div class="col-md-4">
            <select @change="props.trocarFiltro" class="form-select">
              <option value="todas">Todas tarefas</option>
              <option value="pendentes">Pendentes</option>
              <option value="finalizadas">Finalizadas</option>
            </select>
          </div>

        </div>
      </form>
</template>
