<template>
    <div class="bg-gray-900 text-white flex justify-center h-screen p-4">
        <div class="w-full md:w-6/12 border rounded-lg p-6">
            <Header
                @toggle-add-task-pane="toggleAddTaskPane"
                :showAddTask="showAddTask"
            >
                Task Tracker
            </Header>
            <div v-show="showAddTask">
                <AddTask @add-task="addTask" />
            </div>
            <Tasks
                @delete-task="deleteTask"
                @toggle-reminder="toggleReminder"
                :tasks="tasks"
            />
        </div>
    </div>
</template>

<script >
import Header from "./components/Header.vue";
import Tasks from "./components/Tasks.vue";
import AddTask from "./components/AddTask.vue";

export default {
    name: "App",
    components: {
        Header,
        Tasks,
        AddTask,
    },
    data() {
        return {
            tasks: [],
            showAddTask: false,
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
        toggleAddTaskPane() {
            this.showAddTask = !this.showAddTask;
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
