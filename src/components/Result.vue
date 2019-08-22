<template>
  <input ref="input" @keypress="keyPressed" @focus="onFocus" @blur="onBlur" :value="result" title="Result"
         readonly="readonly">
</template>

<script>
  export default {
    name: "Result",
    props: {
      result: {
        require: true
      }
    },
    methods: {
      keyPressed(e) {
        this.$emit('keyPress', e)
      },
      onFocus() {
        this.$emit('onOpen')
      },
      onBlur() {
        this.$emit('onClose')
      }
    }
  }
</script>

<style scoped>
  input {
    box-sizing: border-box;
    border-style: none;
    padding: 35px 30px 25px;
    width: 100%;
    height: 120px;
    background-color: transparent;
    color: #ffffff;
    text-align: right;
    font-size: 84px;
  }
</style>
