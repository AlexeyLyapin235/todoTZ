<template>
  <button :class="[{ red: color === 'red' },{ green: color === 'green' },]" class="custom-button" @click="handleClick">
    {{ title }}
  </button>
</template>
  
<script>
export default {
  name: "CustomButton",
  props: {
    title: {
      type: String
    },
    color: {
      type: String
    }
  },
  methods: {
    handleClick() {
      this.$emit('click');
    }
  }
};
</script>
  
<style scoped lang="scss">
.custom-button{
  border: none;
}
.red{
  background-color: #FF6052;
  color: #EB1400;
}
.green{
  background: #29CC44;
  color: green;
}
</style>
  