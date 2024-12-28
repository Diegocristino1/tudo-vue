<script setup>
    const props = defineProps(["cadastraatividade", "atividadeTemp", "trocarFiltro", "editaAtividadeTemp"])
</script>

<template>
    <form @submit.prevent="props.cadastraAtividade">
    <div class="row">
        <div class="col">
        <input :value="props.atividadeTemp" @change="props => editaAtividadeTempatividadeTemp =  required
            type="text placeholder="Digite aqui a descrição da atividade" class="form-control">
        </div>
        <div class="col-md-2">
        <button type="submit" class="btn btn-primary">Cadastrar</button>
        </div>
        <div class="col-md-2">
        <select @change="evento => props.trocarFiltro" class="form-control">
            <option value="todas">Todas atividades</option>
            <option value="pendentes">Pendentes</option>
            <option value="finalizadas">Finalizadas</option>
        </select>
        </div>
    </div>
    </form>
</template>