<template>
    <button @click="onClick()" class="p-2 pb-3 rounded-lg" :class="bg">
        {{ text }}
    </button>
</template>

<script>
export default {
    name: "Button",
    data() {
        return {};
    },
    props: {
        text: String,
        text: String,
        bg: String,
    },
    methods: {
        onClick() {
            this.$emit("btn-click");
        },
    },
};
</script>