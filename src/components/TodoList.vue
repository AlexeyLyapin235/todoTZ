<template>
    <div class="todo-content">
        <div class="todo-content__form">
            <FormTask @addTask="addTask"></FormTask>
        </div>
      <div class="todo-content__list">
            <div v-for="task in tasks" class="task">
                <div class="todo-text" v-if="!task.edit">{{ task.text }}</div>
                <CustomInput v-if="task.edit" v-model="task.text" />
                <div class="todo-buttons">
                    <CustonButton v-if="!task.edit" @click="deleteTask(task.id)" :title="'удалить задачу'" :color="'red'"></CustonButton>
                    <CustonButton v-if="!task.edit" @click="editTask(task.id)"  :title="'отредактировать'" :color="'green'"></CustonButton>
                    <CustonButton v-if="task.edit" @click="saveTask(task.id)"  :title="'сохранить'" :color="'green'"></CustonButton>
                </div>
            </div>
        </div>
        </div>
</template>
<script>
import CustomInput from '@/components/input/CustomInput.vue';
import CustonButton from '@/components/buttons/CustomButton.vue';
import FormTask from '@/components/forms/FormTask.vue';
export default {
    name: "TodoList",
    components: { FormTask, CustomInput ,CustonButton},
    data() {
        return {
            task: '',
        }
    },
    props:{
        tasks:{
            type:Array,
        }
    },
    methods: {
        deleteTask(id) {
            this.$emit('deleteTask',id)
        },
        saveTask(id) {
            this.$emit('saveTask',id)
        },
        editTask(id) {
            this.$emit('editTask',id)
        },
        addTask(task) {
            this.$emit('addTask',task)
        },
    },
}
</script>
<style lang="scss" scoped>
.todo-content{
    display: flex;
    flex-direction: column;
    align-items: center;
}
</style>