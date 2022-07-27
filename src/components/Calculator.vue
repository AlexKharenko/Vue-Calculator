<template>
  <div class="calculator-container">
    <!-- {{ inputError }} {{ errorMessage }} -->
    <CalculatorScreen
      :resultNumber="resultNumber"
      :inputNumber="inputNumber"
      :currentOperation="currentOperation"
    />
    <div class="buttons-container">
      <FunctionButton :btnFunction="clearAll" span2="true" btnValue="AC" />
      <FunctionButton :btnFunction="clearSymbol" btnValue="C" />
      <FunctionButton :btnFunction="operationClick" btnValue="/" />
      <NumberButton :btnFunction="numberClick" btnValue="1" />
      <NumberButton :btnFunction="numberClick" btnValue="2" />
      <NumberButton :btnFunction="numberClick" btnValue="3" />
      <FunctionButton :btnFunction="operationClick" btnValue="*" />
      <NumberButton :btnFunction="numberClick" btnValue="4" />
      <NumberButton :btnFunction="numberClick" btnValue="5" />
      <NumberButton :btnFunction="numberClick" btnValue="6" />
      <FunctionButton :btnFunction="operationClick" btnValue="-" />
      <NumberButton :btnFunction="numberClick" btnValue="7" />
      <NumberButton :btnFunction="numberClick" btnValue="8" />
      <NumberButton :btnFunction="numberClick" btnValue="9" />
      <FunctionButton :btnFunction="operationClick" btnValue="+" />
      <NumberButton :btnFunction="numberClick" btnValue="." />
      <NumberButton :btnFunction="numberClick" btnValue="0" />
      <FunctionButton :btnFunction="getResult" span2="true" btnValue="=" />
    </div>
  </div>
</template>

<script>
import NumberButton from "@/components/NumberButton.vue";
import FunctionButton from "@/components/FunctionButton.vue";
import CalculatorScreen from "@/components/CalculatorScreen.vue";

export default {
  name: "Calculator",
  data() {
    return {
      allowedChars: {
        numbers: [1, 2, 3, 4, 5, 6, 7, 8, 9, 0],
        operators: ["+", "-", "*", "/"],
        symbols: ["."],
      },
      resultNumber: "",
      inputNumber: "0",
      currentOperation: "",
    };
  },
  components: { CalculatorScreen, NumberButton, FunctionButton },
  computed: {},
  methods: {
    operationClick(operation) {
      this.makeCalculation();
      this.chooseOperation(operation);
    },
    numberClick(number) {
      this.writeSymbol(number, number !== ".");
    },
    writeSymbol(symbol, isNumber) {
      if (this.inputNumber === "0") {
        this.inputNumber = symbol;
        return;
      }
      if (this.inputNumber.includes(".") && !isNumber) return;
      this.inputNumber += symbol;
    },
    clearSymbol() {
      if (this.inputNumber === "") {
        this.currentOperation = "";
        return;
      }
      this.inputNumber = this.inputNumber.slice(0, this.inputNumber.length - 1);
    },
    clearAll() {
      this.inputNumber = "0";
      this.resultNumber = "";
      this.currentOperation = "";
    },
    makeCalculation() {
      if (this.currentOperation != "") {
        const floatResult = parseFloat(this.resultNumber || 0);
        const floatInput = parseFloat(this.inputNumber || 0);
        if (this.currentOperation === "-") {
          this.resultNumber = floatResult - floatInput;
        } else if (this.currentOperation === "+") {
          this.resultNumber = floatResult + floatInput;
        } else if (this.currentOperation === "*") {
          this.resultNumber = floatResult * floatInput;
        } else if (this.currentOperation === "/") {
          this.resultNumber = floatResult / floatInput;
        }
        this.resultNumber = this.resultNumber.toFixed(7).toString();
      }
      if (this.resultNumber === "") {
        this.resultNumber = this.inputNumber;
      }
      this.inputNumber = "";
    },
    getResult() {
      this.makeCalculation();
      this.inputNumber = parseFloat(this.resultNumber).toString();
      this.resultNumber = "";
      this.currentOperation = "";
    },
    chooseOperation(operator) {
      if (operator === "-") {
        this.currentOperation = "-";
        return;
      }
      if (operator === "+") {
        this.currentOperation = "+";
        return;
      }
      if (operator === "*") {
        this.currentOperation = "*";
        return;
      }
      if (operator === "/") {
        this.currentOperation = "/";
        return;
      }
    },
  },
  created() {
    window.addEventListener("keydown", (e) => {
      if (this.allowedChars.numbers.includes(+e.key)) {
        this.writeSymbol(e.key, true);
        return;
      }
      if (this.allowedChars.operators.includes(e.key)) {
        this.makeCalculation();
        this.chooseOperation(e.key);
        return;
      }
      if (this.allowedChars.symbols.includes(e.key)) {
        this.writeSymbol(e.key, false);
        return;
      }
      if (e.key === "=") {
        this.getResult();
        return;
      }
      if (e.key === "Backspace") {
        this.clearSymbol();
      }
    });
  },
};
</script>

<style scoped lang="scss">
.calculator-container {
  display: grid;
  justify-content: center;
  justify-items: stretch;
  .buttons-container {
    display: grid;
    grid-template-columns: repeat(4, minmax(80px, auto));
    grid-template-rows: minmax(80px, auto) repeat(5, 80px);
  }
}
</style>
