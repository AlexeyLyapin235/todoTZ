<template>
    <div class="task-form">
      <label>Заполните форму с задачей</label>
      <custom-input v-model="inputValue"></custom-input> 
      <CustomButton @click="addTask" :title="'Добавить задачу'" :color="'green'"></CustomButton>
    </div>
</template>

<script>
import CustomInput from '../input/CustomInput.vue';
import CustomButton from '../buttons/CustomButton.vue';
  export default {
    components: {
      CustomInput,
      CustomButton
    },
    data() {
      return {
        inputValue: '',
      };
    },
    methods:{
        addTask(){
            this.$emit('addTask',this.inputValue)
            this.inputValue = ''
        }
    }
  };
  </script>

<style lang="scss">
.task-form{
  display: flex;
  flex-direction: column;
  width: 400px;
  gap: 8px;
  margin-bottom: 20px;

}
</style>
  