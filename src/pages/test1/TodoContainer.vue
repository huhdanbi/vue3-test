<script setup>
    import { ref } from 'vue'
    import TodoInput from './components/TodoInput.vue'
    import TodoList from './components/TodoList.vue'

    let todos = ref([])

    const getList = (e) => {
        todos.value = [...todos.value, {msg: e.value}]
    }

    const onUpdate = (idx) => {
        console.log(idx);
    }

    const onDelete = (idx) => {
        todos.value.splice(idx, 1)
    }

</script>

<template>
    <div>
        <todo-input @add-list="getList"/>
        <todo-list :todo-list="todos" @on-update="onUpdate" @on-delete="onDelete" />
    </div>
</template>


