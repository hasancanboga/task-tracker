<template>
    <header class="flex justify-between">
        <h1 class="text-3xl"><slot></slot></h1>
        <Button
            @btn-click="$emit('toggle-add-task-pane')"
            :bg="showAddTask ? 'bg-red-800' : 'bg-green-900'"
            :text="showAddTask ? 'Close' : 'Add Task'"
        />
    </header>
</template>

<script>
import Button from "./Button.vue";
export default {
    name: "Header",
    props: {
        title: String,
        showAddTask: Boolean,
    },
    components: {
        Button,
    },
};
</script>

<style scoped>
</style>
