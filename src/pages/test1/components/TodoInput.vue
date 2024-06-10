<script setup>
    import { ref } from 'vue'
    import BtnDefault from '@/components/common/BtnDefault.vue'

    const todo = ref('')

    const emit = defineEmits(['addList'])

    const addList = () => {
        emit('addList', todo)
        todo.value = ''
    }
    
</script>

<template>
    <div class="box-list">
        <input type="text" v-model="todo" class="inp-todo" placeholder="input text">
        <btn-default name="add" @click="addList" />
    </div>
</template>

<style scoped>
.box-list{display:flex;justify-content:center;padding:0 50px;margin-bottom:20px}
.inp-todo {width:100%;margin-right:7px;padding:0 15px;border:1px solid #dedede;border-radius:5px}

</style>