<template>
    <button @click="onClick()" class="p-2 pb-3 rounded-lg" :class="bg">
        <slot> </slot>
    </button>
</template>

<script>
export default {
    name: "Button",
    data() {
        return {};
    },
    props: {
        bg: String,
    },
    methods:{
        onClick(){
            
        }
    }
}
</script>