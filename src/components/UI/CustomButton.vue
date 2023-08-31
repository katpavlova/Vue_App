<script>
  export default {
    name: 'custom-button',

  }
</script>

<template>
  <button class="form__btn">
    <slot></slot>
  </button>
</template>

<style scoped>
.form__btn{
  color: #FFF;
  font-size: 20px;
  font-style: normal;
  font-weight: 700;
  line-height: 150%;
  border: none;
  border-radius: 9px;
  background: #5B98E3;
  padding: 12px 8px 14px 8px;
  outline: none;
  width: 95%;
}
</style>