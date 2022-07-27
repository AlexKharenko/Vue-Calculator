<template>
  <div class="screen-container">
    <span class="result-block">{{ formatedResultNumber }}</span>
    <div class="input-block">
      <span class="operator">{{ currentOperation }}</span>
      <span class="input-number">{{ formatedInputNumber }}</span>
    </div>
  </div>
</template>

<script>
export default {
  name: "CalculatorScreen",
  props: ["resultNumber", "inputNumber", "currentOperation"],
  computed: {
    formatedResultNumber() {
      if (this.resultNumber === "") return "";
      return parseFloat(this.resultNumber).toLocaleString("en-US", {
        maximumFractionDigits: 7,
      });
    },
    formatedInputNumber() {
      if (this.inputNumber === "") return "";
      if (this.inputNumber.includes(".")) {
        const [beforePoint, afterPoint] = this.inputNumber.split(".");
        return `${(+beforePoint || 0).toLocaleString("en-US")}.${
          afterPoint ? afterPoint : ""
        }`;
      }
      return parseFloat(this.inputNumber).toLocaleString("en-US");
    },
  },
};
</script>

<style lang="scss" scoped>
.screen-container {
  height: 80px;
  padding: 20px 10px;
  background-color: rgb(41, 40, 40);
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  font-size: 1.55rem;
  align-items: flex-end;
  span {
    color: white;
  }

  .result-block {
    font-size: 1.2rem;
    color: gray;
  }
  .input-block {
    display: flex;
    width: 100%;
    justify-content: space-between;
  }
}
</style>
