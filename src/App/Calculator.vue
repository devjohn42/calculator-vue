<template>
  <div class="calculator">
    <Display :value="displayValue" />
    <Button label="AC" triple @onButtonClick="clearMemory" />
    <Button label="/" operation @onButtonClick="setOperation" />
    <Button label="7" @onButtonClick="addValue" />
    <Button label="8" @onButtonClick="addValue" />
    <Button label="9" @onButtonClick="addValue" />
    <Button label="*" operation @onButtonClick="setOperation" />
    <Button label="4" @onButtonClick="addValue" />
    <Button label="5" @onButtonClick="addValue" />
    <Button label="6" @onButtonClick="addValue" />
    <Button label="-" operation @onButtonClick="setOperation" />
    <Button label="1" @onButtonClick="addValue" />
    <Button label="2" @onButtonClick="addValue" />
    <Button label="3" @onButtonClick="addValue" />
    <Button label="+" operation @onButtonClick="setOperation" />
    <Button label="0" double @onButtonClick="addValue" />
    <Button label="." @onButtonClick="addValue" />
    <Button label="=" operation @onButtonClick="setOperation" />
  </div>
</template>

<script>
import Button from "../components/Button.vue";
import Display from "../components/Display.vue";

export default {
  data: () => {
    return {
      displayValue: "0",
      clearDisplay: false,
      operation: null,
      values: [0, 0],
      current: 0,
    };
  },

  components: { Button, Display },
  methods: {
    clearMemory() {
      //atribuindo ao data o estado inicial do objeto
      Object.assign(this.$data, this.$options.data());
    },

    setOperation(operation) {
      if (this.current === 0) {
        this.operation = operation;
        this.current = 1;
        this.clearDisplay = true;
      } else {
        const equals = operation === "=";
        const currentOperation = this.operation;

        try {
          this.values[0] = eval(
            `${this.values[0]} ${currentOperation} ${this.values[1]}`
          );
          if (isNaN(this.values[0]) || !isFinite(this.values[0])) {
            this.clearMemory();
            return;
          }
        } catch (error) {
          this.$emit("onError", error);
        }

        this.values[1] = 0;

        this.displayValue = this.values[0].toFixed(2);
        this.operation = equals ? null : operation;
        this.current = equals ? 0 : 1;
        this.clearDisplay = !equals;
      }
    },
    addValue(value) {
      if (value === "." && this.displayValue.includes(".")) {
        return;
      }

      const clearDisplay = this.displayValue === "0" || this.clearDisplay;
      const currentValue = clearDisplay ? "" : this.displayValue;
      const displayValue = currentValue + value;

      this.displayValue = displayValue;
      this.clearDisplay = false;
      // this.values[this.current] = displayValue;

      //utilizar essa lógica caso queira substituir o eval pelo switch

      if (value !== ".") {
        const i = this.current;
        const newValue = parseFloat(displayValue);
        this.values[i] = newValue;
        console.log(displayValue);
      }
    },
  },
};
</script>

<style>
.calculator {
  height: 320px;
  width: 235px;
  border-radius: 5px;
  overflow: hidden;

  display: grid;
  grid-template-columns: repeat(4, 25%);
  grid-template-rows: 1fr repeat(5, 48px);
}
</style>
