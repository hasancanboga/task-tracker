<template>
    <header class="flex justify-between">
        <h1 class="text-3xl"><slot></slot></h1>
        <Button bg="bg-green-900"> Add Task </Button>
    </header>
</template>

<script>
import Button from "./Button.vue";
export default {
    name: "Header",
    props: {
        title: String,
    },
    components: {
        Button,
    },
};
</script>

<style scoped>
</style>
