<template>
    <form @submit="onSubmit" class="add-form px-4 flex-col space-y-4 my-6">
        <div class="">
            <label class="sr-only">Task</label>
            <input
                v-model="text"
                class="bg-gray-900 border-2 w-full p-2 rounded-lg"
                type="text"
                name="text"
                placeholder="Add Task"
            />
        </div>
        <div class="">
            <label class="sr-only">Day & Time</label>
            <input
                v-model="day"
                class="bg-gray-900 border-2 w-full p-2 rounded-lg"
                type="text"
                name="day"
                placeholder="Add Day & Time"
            />
        </div>
        <div class="">
            <label class="inline-flex items-center mt-3">
                <input
                    v-model="reminder"
                    type="checkbox"
                    class="form-checkbox h-5 w-5 text-green-600"
                    checked
                /><span class="ml-2 text- white">Set Reminder</span>
            </label>
        </div>

        <input
            type="submit"
            value="Save Task"
            class="bg-blue-800 text-white px-4 py-3 rounded font-medium w-full"
        />
    </form>
</template>

<script>
export default {
    name: "AddTask",
    data() {
        return {
            text: "",
            day: "",
            reminder: false,
        };
    },
    methods: {
        onSubmit(e) {
            e.preventDefault();
            if (!this.text) {
                alert("Please add a task");
                return;
            }
            const newTask = {
                // id: Math.floor(Math.random() * 10000),
                text: this.text,
                day: this.day,
                reminder: this.reminder,
            };
            this.$emit('add-task', newTask)
            this.text = "";
            this.day = "";
            this.reminder = false;
        },
    },
};
</script>

<style scoped></style>