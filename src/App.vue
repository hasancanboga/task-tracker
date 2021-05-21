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
        addTask(task) {
            this.tasks = [...this.tasks, task];
        },
        deleteTask(task) {
            this.tasks = this.tasks.filter((t) => t.id !== task.id);
        },
        toggleReminder(task) {
            this.tasks = this.tasks.map((t) =>
                t.id === task.id ? { ...t, reminder: !t.reminder } : t
            );
        },
        toggleAddTaskPane() {
            this.showAddTask = !this.showAddTask;
        },
    },
    created() {
        this.tasks = [
            {
                id: 1,
                text: "Doctors Appointment",
                day: "March 1st at 2:30pm",
                reminder: true,
            },
            {
                id: 2,
                text: "Meeting at School",
                day: "March 3rd at 1:30pm",
                reminder: true,
            },
            {
                id: 3,
                text: "Doctors Appointment",
                day: "March 3 at 11:00am",
                reminder: false,
            },
        ];
    },
};
</script>

<style>
</style>
