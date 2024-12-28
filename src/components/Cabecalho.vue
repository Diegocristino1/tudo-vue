<script setup>
const props = defineProps(["atividadespendentes"])
</script>
<template>
    <header class="p-5 mb-4 mt-4 bg-light rounded-3">
        <h1>Minhas Atividades</h1>
        <p>
        Vocé possui {{ props.atividadespendentes }} atividades pendentes
        </p>
    </header>
</template>