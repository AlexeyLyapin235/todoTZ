<template>
    <div class="todo-page">
        <TodoList 
          @deleteTask="deleteTask"
          @editTask="editTask" 
          @saveTask="saveTask" 
          @addTask="addTask" 
          :tasks="taskList">
        </TodoList>
    </div>
</template>
  
<script>
import FormTask from '@/components/forms/FormTask.vue';
import { mapMutations, mapState } from 'vuex';
import CustomInput from '@/components/input/CustomInput.vue';
import CustonButton from '@/components/buttons/CustomButton.vue'
import TodoList from '@/components/TodoList.vue';
export default {
    name: "TaskList",
    components: { FormTask, CustomInput, CustonButton, TodoList },
    data() {
        return {
            taskList: [],
        }
    },
    computed: {
        ...mapState({
            tasks: state => state.tasks
        })
    },
    mounted() {
        if (localStorage.getItem('tasks')) {
            const json = JSON.parse(localStorage.getItem('tasks'))
            this.taskList = json
        }
    },
    methods: {
        replaceLocalStorage(taskList) {
            const json = JSON.stringify(taskList)
            localStorage.setItem('tasks', json)
            this.setTask(taskList)
        },
        deleteTask(id) {
            this.taskList = this.taskList.filter((el) => el.id !== id)
            this.replaceLocalStorage(this.taskList)
        },
        saveTask(id) {
            const index = this.taskList.findIndex((el) => el.id === id)
            if (index !== -1 && this.taskList[index].text === '') {
                alert('Пожалуйста заполните таску ,таска не может быть пустой ')
                return
            }
            if (index !== -1 && this.taskList[index].edit === true) {
                this.$set(this.taskList[index], 'edit', false)
                this.replaceLocalStorage(this.taskList)
            }
        },
        editTask(id) {
            const index = this.taskList.findIndex((el) => el.id === id)
            if (index !== -1) {
                this.$set(this.taskList[index], 'edit', true)
                this.replaceLocalStorage(this.taskList)
            }
        },
        addTask(task) {
            if (task === '') {
                return
            }
            const obj = {
                text: task,
                id: Date.now(),
                edit: false
            }
            this.taskList.push(obj)
            this.replaceLocalStorage(this.taskList)
        },
        ...mapMutations({
            setTask: 'SET_TASK',

        })
    },
}
</script>
  