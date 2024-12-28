<script setup>
import { reactive } from 'vue';

  const estado = reactive ({
    filtro: "todas",
    atividadeTemp: "",
    atividade: [
      {
        titulo: "Estudar Python",
        finalizada: false,
      },

      {
        titulo: "Estudar SASS",
        finalizada: false,
      },

      {
        titulo: "Ir para a academia",
        finalizada: true,
      }
    ]
  })

  const getAtividadesPendentes = () => {
    return estado.atividade.filter(atividade => !atividade.finalizada)
  }

  const getAtividadesfinalizadas = () => {
    return estado.atividade.filter(atividade => atividade.finalizada)
  }
  const getAtividadesFiltradas = () => {
    const { filtro } = estado;

    switch ( filtro ) {
      case "pendentes":
        return getAtividadesPendentes();
        case "finalizadas":
          return getAtividadesfinalizadas();
          default:
            return estado.atividade;
    }
  }

  const cadastraAtividade = () => {
    const atividadeNova = {
      titulo: estado.atividadeTemp,
      finalizada: false,
    }
    estado.atividade.push(atividadeNova);
    estado.atividadeTemp = "";
  }
</script>

<template>
  <div class="container">
    <header class="p-5 mb-4 mt-4 bg-light rounded-3">
      <h1>Minhas Atividades</h1>
      <p>
        Vocé possui {{ getAtividadesPendentes().length }} atividades pendentes
      </p>
    </header>
  <form @submit.prevent="cadastraAtividade">
    <div class="row">
      <div class="col">
        <input :value="estado.atividadeTemp" @change="evento => estado.atividadeTemp = evento.target.value" required type="text" placeholder="Digite a descrição da atividade" class="form-control">
      </div>
      <div class="col-md-2">
        <button type="submit" class="btn btn-primary">Cadastrar</button>
      </div>
      <div class="col-md-2">
        <select @change="evento => estado.filtro = evento.target.value" class="form-control">
          <option value="todas">Todas atividades</option>
          <option value="pendentes">Pendentes</option>
          <option value="finalizadas">Finalizadas</option>
        </select>
      </div>
    </div>
  </form>
  <ul class="list-group mt-4">
    <li class="list-group-item" v-for="atividade in getAtividadesFiltradas">
      <input @change="evento => atividade.finalizada = evento.target.checked" :checked="atividade.finalizada" :id="atividade.titulo" type="checkbox">
      <label :class="{ done: atividade.finalizada }" class="ms-3" :for="atividade.titulo">
        {{ atividade.titulo }}
      </label>
    </li>
  </ul>
  </div>
</template>

<style scoped>
.done {
  text-decoration: line-through;
}
</style>
