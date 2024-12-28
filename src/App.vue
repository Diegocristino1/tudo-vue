<script setup>
import { reactive } from 'vue';
import Cabecalho from './components/Cabecalho.vue';
import Formulario from './components/Formulario.vue';
import listaDeTarefas from './components/listaDeTarefas.vue';

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
    <Cabecalho :atividades-pendentes="getAtividadesPendentes().length" />
    <Formulario :trocar-filtro="evento => estado.filtro = evento.target.value" :atividade-temp="estado.atividadeTemp" :edita-atividade-temp="evento => estado.atividadeTemp = evento.target.value" :cadastraatividade="cadastraAtividade" />
    <listaDeTarefas :atividades="getAtividadesFiltradas()" />
  </div>
</template>


