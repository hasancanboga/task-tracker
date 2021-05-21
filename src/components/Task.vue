<template>
    <div @dblclick="$emit('toggle-reminder', task)"
        :class="[
            task.reminder ? 'border-l-8 border-green-700' : '',
            'bg-gray-700 m-4 rounded p-3',
        ]"
    >
        <div class="flex justify-between">
            <h3 class="text-xl">{{ task.text }}</h3>
            <i @click="$emit('delete-task', task)" class="fas fa-times text-red-400"></i>
        </div>
        <p>{{ task.day }}</p>
    </div>
</template>

<script>
export default {
    name: "Task",
    props: {
        task: Object,
    },
    methods: {
    },
};
</script>