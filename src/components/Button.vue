<template>
  <button
    class="button"
    @click="$emit('onButtonClick', label)"
    :class="{ double, triple, operation }"
  >
    {{ label }}
  </button>
</template>

<script>
export default {
  props: {
    label: {},
    operation: { type: Boolean },
    double: { type: Boolean },
    triple: { type: Boolean },
  },
};
</script>

<style>
:root {
  --bg-button: #f5f5f5;
  --border-button: solid 1px #777;
}

.button {
  background-color: var(--bg-button);
  font-size: 1.4rem;
  cursor: pointer;
  border: none;
  outline: none;
  border-right: var(--border-button);
  border-bottom: var(--border-button);
}

.button:hover {
  background-color: #cccccc;
}

.button:active {
  background-color: #888888;
}

.button.double {
  grid-column: span 2;
}

.button.triple {
  grid-column: span 3;
}

.button.operation {
  background-color: #2d2d2d;
  color: white;
}

.button.operation:hover {
  background-color: #813535;
}
.button.operation:active {
  background-color: #811e1e;
}
</style>
