<script>
  export default {
    name: "custom-input",
    props: {
      modelValue: [String, Number]
    },
    methods: {
      updateInput(event){
        this.$emit('update:modelValue', event.target.value);
      },
    },
  }

</script>

<template>
  <input type="text" class="form__input" :value="modelValue" @input="updateInput">
</template>

<style scoped>
.form__input{
  color: #000;
  font-size: 18px;
  font-style: normal;
  font-weight: 400;
  line-height: 150%;
  padding: 12px 8px 14px 8px;

  border-radius: 5px;
  border: 1px solid #FFF;
  background: #FFF;
  outline: none;
  width: 95%;
}
</style>