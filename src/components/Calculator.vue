<template>
  <div class="calculator">
    <Result :result="result" @keyPress='keyPress' @onOpen="onOpen" @onBlur="onClose"></Result>
    <KeyButton @btnClick="btnClick"></KeyButton>
  </div>
</template>

<script>
  import Result from '@/components/Result'
  import KeyButton from '@/components/KeyButton'

  export default {
    name: "Calculator",
    components: {Result, KeyButton},
    data() {
      return {
        left: 0,
        oper: '',
        is_new_input: true,
        result: '0',
        keyButton: false
      }
    },
    methods: {
      btnClick(btn) {
        if (btn >= '0' && btn <= '9' || btn === '.') {
          this.appendText(btn)
        } else if (btn === '+' || btn === '-' || btn === '*' || btn === '/') {
          this.btnOper(btn)
        } else if (btn === '%') {
          this.btnPercentage(btn)
        } else if (btn === '=') {
          this.btnResult(btn)
        } else if (btn === '+/-') {
          this.btnChange(btn)
        } else if (btn === 'AC') {
          this.btnClear()
        } else if (btn === '<') {
          this.btnDel()
        }
      },

      //键盘输入
      keyPress(e) {
        if ((e.key >= '0' && e.key <= '9') || e.key === '.') {
          this.appendText(e.key)
        } else if (e.key === '+' || e.key === '-') {
          this.btnOper(e.key)
        } else if (e.key === '*') {
          this.btnOper('*')
        } else if (e.key === '/') {
          this.btnOper('/')
        } else if (e.key === '%') {
          this.btnPercentage()
        } else if (e.key === 'Enter' || e.key === 'Return' || e.key === '=') {
          this.btnResult()
        }
      },

      appendText(number) {
        if (this.is_new_input) {
          this.clearText()
          this.is_new_input = false
        }
        if (this.result === '0' && number !== '.') {
          this.result = ''
        }
        // 设置只能输入一个小数点
        if (number === '.' && this.result.indexOf('.') !== -1) {
          return
        }
        // 如果输入框中字符小于7个才能继续输入
        if (this.result.length < 7) {
          this.result += number
        }
      },

      btnDel() {
        let delRes = this.result
        this.result = delRes.substr(0, delRes.length - 1)
      },
      //清除
      btnClear() {
        if (this.clearButton === 'AC') {
          this.reset()
        }
        this.clearText()
      },

      //改变符号
      btnChange() {
        if (this.result !== 'ERROR') {
          this.result = this.fixFloat(this.result *= -1)
        }
      },

      //添加%
      btnPercentage() {
        if (this.result !== 'ERROR') {
          this.result = this.fixFloat(this.result *= 0.01)
        }
      },
      //计算
      btnOper(oper) {
        if (this.result !== 'ERROR') {
          this.btnResult()
          this.left = parseFloat(this.result)
          this.oper = oper
          this.is_new_input = true
        }
      },
      //进行计算
      btnResult() {
        let right = parseFloat(this.result)
        if (this.oper !== '' && this.is_new_input !== true) {
          let res
          switch (this.oper) {
            case '+':
              res = this.left + right
              break
            case '-':
              res = this.left - right
              break
            case '*':
              res = this.left * right
              break
            case '/':
              if (right === 0) {
                res = 'ERROR'
              } else {
                res = this.left / right
              }
              break
            default:
              res = 'ERROR'
          }
          if (res !== 'ERROR') {
            this.result = this.fixFloat(res)
          } else {
            this.result = 'ERROR'
          }
          this.clearButton = 'AC'
        }
        this.reset()
      },
      fixFloat(float) {
        float = float.toFixed(5)
        float.replace(/0+$/, '')
        return parseFloat(float).toString()
      },
      reset() {
        this.left = 0
        this.oper = ''
        this.is_new_input = true
      },
      clearText() {
        this.result = '0'
        this.clearButton = 'AC'
      },
      onOpen() {
        this.keyButton = true
      },
      onClose() {
        this.keyButton = false
      }
    },
    mounted() {
      this.clearText()
    }
  }
</script>

<style scoped>
  .calculator {
    display: flex;
    box-sizing: border-box;
    margin: 100px auto;
    padding: 1px;
    width: 50%;
    max-width: 430px;
    border-radius: 10px;
    background-color: #999;
    box-shadow: 0 3px 6px rgba(0, 0, 0, 0.16), 0 3px 6px rgba(0, 0, 0, 0.23);
    flex-direction: row;
    flex-wrap: wrap;
  }
</style>
