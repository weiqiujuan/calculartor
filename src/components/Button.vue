<template>
  <button @click="btnClick">{{btnText}}</button>
</template>

<script>
  export default {
    name: "Button",
    props: {
      btnText: {
        require: true
      }
    },
    methods: {
      btnClick() {
        this.$emit('btnClick', this.btnText)
      }
    }
  }
</script>

<style scoped>
  button {
    margin: 1px;
    height: 85px;
    width: 100px;
    flex: 1;
    border-style: none;
    text-align: center;
    cursor: pointer;
  }
  button:focus{
    outline: none;
  }
</style>
