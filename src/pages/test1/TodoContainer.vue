<script setup>
    import { ref } from 'vue'
    import TodoInput from './components/TodoInput.vue'
    import TodoList from './components/TodoList.vue'

    let todos = ref([])

    const getList = (e) => {
        todos.value = [...todos.value, {msg: e.value, isUpdate: false, isDisabled: false }]
    }

    const setUpdateDisabled = () => {
        todos.value.map(e => {
            e.isDisabled = !e.isDisabled
        })
    }

    const onUpdate = (idx) => {
        todos.value[idx].isUpdate = true
        setUpdateDisabled();
        todos.value[idx].isDisabled = false
    }

    const onDelete = (idx) => {
        todos.value.splice(idx, 1)
    }

    const onConfirm = (res) => {
        todos.value[res.idx].msg = res.msg
        onCancel(res.idx)
    }

    const onCancel = (idx) => {
        setUpdateDisabled()
        todos.value[idx].isUpdate = false
        todos.value[idx].isDisabled = false
    }

</script>

<template>
    <div>
        <todo-input @add-list="getList" :is-update="isUpdate"/>
        <todo-list :todo-list="todos" @on-update="onUpdate" @on-delete="onDelete" @on-confirm="onConfirm" @on-cancel="onCancel" />
    </div>
</template>


