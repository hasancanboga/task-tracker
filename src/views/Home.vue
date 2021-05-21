<template>
    <AddTask v-show="showAddTask" @add-task="addTask" />
    <Tasks
        @delete-task="deleteTask"
        @toggle-reminder="toggleReminder"
        :tasks="tasks"
    />
</template>

<script>
import Tasks from "../components/Tasks.vue";
import AddTask from "../components/AddTask.vue";

export default {
    name: "Home",
    props: {
        showAddTask: Boolean,
    },
    components: {
        Tasks,
        AddTask,
    },
    data() {
        return {
            tasks: [],
        };
    },
    methods: {
        async addTask(task) {
            const res = await fetch("api/tasks", {
                method: "post",
                headers: {
                    "Content-type": "application/json",
                },
                body: JSON.stringify(task),
            });

            const data = await res.json();
            this.tasks = [...this.tasks, data];
        },
        async deleteTask(task) {
            if (confirm("Are you sure?")) {
                const res = await fetch(`api/tasks/${task.id}`, {
                    method: "delete",
                });

                res.status === 200
                    ? (this.tasks = this.tasks.filter((t) => t.id !== task.id))
                    : alert("Error deleting task.");
            }
        },
        async toggleReminder(task) {
            const updTask = { ...task, reminder: !task.reminder };

            const res = await fetch(`api/tasks/${task.id}`, {
                method: "PUT",
                headers: {
                    "Content-type": "application/json",
                },
                body: JSON.stringify(updTask),
            });
            const data = await res.json();
            this.tasks = this.tasks.map((t) =>
                t.id === task.id ? { ...t, reminder: data.reminder } : t
            );
        },
        async fetchTasks() {
            const res = await fetch("api/tasks");
            const data = await res.json();
            return data;
        },
        async fetchTask() {
            const res = await fetch(`api/tasks/${id}`);
            const data = await res.json();
            return data;
        },
    },
    async created() {
        this.tasks = await this.fetchTasks();
    },
};
</script>

<style>
</style>