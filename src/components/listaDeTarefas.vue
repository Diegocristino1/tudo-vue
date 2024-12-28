<script setup>
    const props = defineProps(["atividades"]);
</script>

<template>
    <ul class="list-group mt-4">
    <li class="list-group-item" v-for="atividade in props.atividades">
        <input @change="evento => atividade.finalizada = evento.target.checked" :checked="atividade.finalizada" :id="atividade.titulo" type="checkbox">
        <label :class="{ done: atividade.finalizada }" class="ms-3" :for="atividade.titulo">
        {{ atividade.titulo }}
        </label>
    </li>
    </ul>
</template>

<style scoped>
    .done {
    text-decoration: line-through;
    }
</style>