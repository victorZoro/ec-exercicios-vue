<script setup>
const props = defineProps(['text']);
</script>

<template>
    <button class="btn">{{ props.text }}</button>
</template>

<style scoped>
</style>