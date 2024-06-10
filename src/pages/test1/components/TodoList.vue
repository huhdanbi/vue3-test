<script setup>
    import { reactive, inject } from 'vue'
    import BtnDefault from '@/components/common/BtnDefault.vue'

    const emit = defineEmits(['onUpdate', 'onDelete'])
    const swal = inject('$swal')

    defineProps({
        todoList :{
            type: Array,
            default: () => []
        }
    })

    let updateData = reactive({})

    const onInput = (msg, idx) => {
        updateData = {msg, idx}
    }

    const onCancel = (idx) => {
        emit('onCancel', idx)
    }

    const onConfirm = () => {
        if( updateData.msg.length < 1 ){
            swal('check input')
            return false
        }
        emit('onConfirm', updateData)
    }

    const onUpdate = (idx) => {
        onInput('', idx)
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
                class="list-todo"
            >
                <div v-if="!item.isUpdate">
                    {{ item.msg }}
                </div>

                <div v-else>
                    <input @input="(e) => onInput(e.target.value, i)" type="text" class="inp-default">
                </div>
                
                <template v-slot:append>
                    <div v-if="!item.isUpdate">
                        <btn-default class="btn-update" name="update" icon="fa-pen-to-square" @click="onUpdate(i)" :disabled="item.isDisabled" />
                        <btn-default class="btn-remove" name="delete" icon="fa-trash" @click="onDelete(i)"/>    
                    </div>

                    <div v-else>
                        <btn-default class="btn-update" name="confirm" icon="fa-solid fa-check" @click="onConfirm(i)"/>    
                        <btn-default class="btn-remove" name="cancel" icon="fa-solid fa-xmark" @click="onCancel(i)"/>    
                    </div>
                </template>

            </v-list-item>
        </v-list>
    </v-card>
</template>

<style scoped>
.v-list-subheader{font-weight:bold;color:#000}

.wrap-list{margin:0 50px}
.list-todo{border-top:1px solid #dedede}

.inp-default{border:1px solid #dedede}
</style>

