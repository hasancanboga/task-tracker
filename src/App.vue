<template>
    <div class="flex justify-center p-4">
        <div class="w-full md:w-6/12 border rounded-lg p-6">
            <Header
                @toggle-add-task-pane="toggleAddTaskPane"
                :showAddTask="showAddTask"
            >
                Task Tracker
            </Header>
            <router-view :showAddTask="showAddTask"></router-view>
            <Footer />
        </div>
    </div>
</template>

<script >
import Header from "./components/Header.vue";
import Footer from "./components/Footer.vue";

export default {
    name: "App",
    components: {
        Header,
        Footer,
    },
    data() {
        return {
            showAddTask: false,
        };
    },
    methods: {
        toggleAddTaskPane() {
            this.showAddTask = !this.showAddTask;
        },
    },
};
</script>

<style>
</style>
