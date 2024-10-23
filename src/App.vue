<template>
  <div class="calculator">
    <input type="text" v-model="display" class="display" disabled />

    <div class="buttons">
      <button
        v-for="btn in buttons"
        :key="btn.value"
        @click="update(btn)"
        :class="`button button_${btn.type || 'default'}`"
      >
        {{ btn.value }}
      </button>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";

const display = ref("");
const buttons = [
  { value: "AC", type: "clear" },
  { value: "DEL", type: "delete" },
  { value: ".", type: "operator" },
  { value: "/", type: "operator" },

  { value: "7" },
  { value: "8" },
  { value: "9" },
  { value: "*", type: "operator" },

  { value: "4" },
  { value: "5" },
  { value: "6" },
  { value: "-", type: "operator" },

  { value: "1" },
  { value: "2" },
  { value: "3" },
  { value: "+", type: "operator" },

  { value: "000" },
  { value: "00" },
  { value: "0" },
  { value: "=", type: "equals" },
];

const update = (btn) => {
  if (btn.type == "clear") {
    return (display.value = "");
  }
  if (btn.type == "delete") {
    return (display.value = display.value.slice(0, -1));
  }
  if (btn.type == "equals") {
    return (display.value = eval(display.value));
  }

  const lastChar = display.value.slice(-1);
  const lastCharISOperator = buttons.some(
    (b) => b.value == lastChar && b.type == "operator"
  );

  if (lastCharISOperator && btn.type == "operator") {
    return;
  }

  display.value += btn.value;
};
</script>

<style scoped></style>
