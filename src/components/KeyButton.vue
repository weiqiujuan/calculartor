<template>
  <div class="keyButton">
    <Button class="btn" btnText="AC" @btnClick="btnClick"></Button>
    <Button class="btn" btnText="+/-" @btnClick="btnClick"></Button>
    <Button class="btn" btnText="%" @btnClick="btnClick"></Button>
    <Button class="btn-operator" btnText="/" @btnClick="btnClick"></Button>


    <Button class="btn-num" btnText="7" @btnClick="btnClick"></Button>
    <Button class="btn-num" btnText="8" @btnClick="btnClick"></Button>
    <Button class="btn-num" btnText="9" @btnClick="btnClick"></Button>
    <Button class="btn-operator" btnText="*" @btnClick="btnClick"></Button>

    <Button class="btn-num" btnText="4" @btnClick="btnClick"></Button>
    <Button class="btn-num" btnText="5" @btnClick="btnClick"></Button>
    <Button class="btn-num" btnText="6" @btnClick="btnClick"></Button>
    <Button class="btn-operator" btnText="-" @btnClick="btnClick"></Button>

    <Button class="btn-num" btnText="1" @btnClick="btnClick"></Button>
    <Button class="btn-num" btnText="2" @btnClick="btnClick"></Button>
    <Button class="btn-num" btnText="3" @btnClick="btnClick"></Button>
    <Button class="btn-operator" btnText="+" @btnClick="btnClick"></Button>

    <Button class="btn-change btn-bottom-left" btnText="<" @btnClick="btnClick"></Button>
    <Button class="btn-num" btnText="0" @btnClick="btnClick"></Button>
    <Button class="btn-num" btnText="." @btnClick="btnClick"></Button>
    <Button class="btn-result btn-bottom-right" btnText="=" @btnClick="btnClick"></Button>
  </div>
</template>

<script>
  import Button from '@/components/Button'

  export default {
    name: "KeyButton",
    components: {Button},
    methods: {
      btnClick(btn) {
        this.$emit('btnClick', btn)
      }
    }
  }
</script>

<style scoped>
  .keyButton {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
    width: 100%;

  }

  .btn-operator, .btn-result, .btn-change {
    background-color: #f69232;
    color: #fff;
    font-size: 36px;
  }

  .btn {
    background-color: #d6d6d6;
    font-size: 36px;
  }

  .btn-num {
    background-color: #e0e0e0;
    font-size: 36px;
  }

  .btn-bottom-left {
    border-radius: 0 0 0 9px;
  }

  .btn-bottom-right {
    border-radius: 0 0 9px 0;
  }
</style>
