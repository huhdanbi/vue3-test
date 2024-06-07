<script setup>
    import { defineProps } from 'vue'

    defineProps({
        name: {
            type: String,
            default: 'Default Name'
        },
        size: {
            type: String,
            default: 'large'
        },
        icon: {
            type: String,
            default: null
        },
    })

</script>

<template>
   <v-btn class="btn-default btn-primary no-uppercase" :size="size" flat user >
        <template v-if="icon">
            <v-tooltip
                activator="parent"
                location="top"
            >
                {{ name }}
            </v-tooltip>
            <v-icon :icon="icon"></v-icon>
        </template>
        <template v-else>
            {{ name }}
        </template>
   </v-btn>
</template>

<style scoped>
    .no-uppercase {
        text-transform: unset !important;
    }

    .btn-default{min-width:40px;margin-left:5px}
    .btn-default:first-child{margin-left:0}

    .btn-primary{background-color:#4d8dee;color:#fff}
    .btn-update{background-color:rgb(138, 138, 138)}
    .btn-remove{background-color:rgb(255, 67, 67)}
</style>