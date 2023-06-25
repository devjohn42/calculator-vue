<template>
  <div class="calculator">
    <Display value="1000" />
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
  components: { Button, Display },
  methods: {
    clearMemory() {
      console.log("Limpar Memória!");
    },
    setOperation(operation) {
      console.log("Operação " + operation);
    },
    addValue(value) {
      console.log("Valor " + value);
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
