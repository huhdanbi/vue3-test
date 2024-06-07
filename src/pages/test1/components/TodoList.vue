<script setup>
    import { defineProps, defineEmits, inject } from 'vue'
    import BtnDefault from '@/components/common/BtnDefault.vue'

    const emit = defineEmits(['onUpdate', 'onDelete'])
    const swal = inject('$swal')

    defineProps({
        todoList :{
            type: Array,
            default: () => []
        }
    })

    const onUpdate = (idx) => {
        emit('onUpdate', idx)
    }

    const onDelete = (idx) => {
        swal({
            title: 'DELETE',
            text: 'Are you sure you want to delete it?',
            showCancelButton: true,
        }).then((res) => {
            if( res.isConfirmed ) emit('onDelete', idx)
        })

        
    }
</script>


<template>
    <v-card class="wrap-list">
        <v-list>
            <v-list-subheader>Todo List</v-list-subheader>

            <v-list-item
                v-for="(item, i) in todoList"
                :key="i"
                :title="item.msg"
                class="list-todo"
            >
                <template v-slot:append>
                    <btn-default class="btn-update" name="update" icon="fa-pen-to-square" @click="onUpdate(i)" />
                    <btn-default class="btn-remove" name="delete" icon="fa-trash" @click="onDelete(i)"/>
                </template>

            </v-list-item>
        </v-list>
    </v-card>
</template>

<style scoped>
.v-list-subheader{font-weight:bold;color:#000}

.wrap-list{margin:0 50px}
.list-todo{border-top:1px solid #dedede}

</style>

