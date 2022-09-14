<script setup>
import { ref } from "vue";

const result = ref(0);
const current = ref(0);

// Clear all calculations
function clear() {
  result.value = 0;
  current.value = 0;
}

// Add numbers and dot to calculations
function appendnum(number) {
  if (result.value === 0) {
    if (number == ".") {
      result.value += number;
    } else if (number != 0) {
      result.value = number;
      current.value = eval(result.value);
    }
  } else {
    // checking not *dot* continuous
    if (
      result.value.toString().charAt(result.value.toString().length - 1) !=
        "." ||
      number != "."
    ) {
      result.value += number;
      current.value = eval(result.value);
    }
  }
}

// Add operations to calculations
function appendOperation(operation) {
  //  A condition exists when the operator is not immediately after the previous operator
  if (
    result.value.toString().charAt(result.value.toString().length - 1) != "+" &&
    result.value.toString().charAt(result.value.toString().length - 1) != "-" &&
    result.value.toString().charAt(result.value.toString().length - 1) != "*" &&
    result.value.toString().charAt(result.value.toString().length - 1) != "/"
  ) {
    if (result.value === 0 || result.value === ".") {
      if (operation == "-") {
        result.value = operation;
        return;
      } else {
        result.value = result.value;
        return;
      }
    }
    result.value += operation;
  }
}

// This function gives the final value of the calculations
function evaluate() {
  result.value = eval(result.value);
}

// remove the last character of calculations
function removeLastCharCalculations() {
  if (result.value != 0) {
    result.value = result.value.toString().slice(0, -1);

    //  If all calculations are cleared, the final value will be zero
    if (result.value == "") {
      result.value = 0;
    }

    //  If the last character was the final value of the operator, we remove the operator from the last character of the current value to display the current value correctly.
    if (
      result.value.toString().charAt(result.value.toString().length - 1) ==
        "+" ||
      result.value.toString().charAt(result.value.toString().length - 1) ==
        "-" ||
      result.value.toString().charAt(result.value.toString().length - 1) ==
        "*" ||
      result.value.toString().charAt(result.value.toString().length - 1) == "/"
    ) {
      current.value = eval(result.value.toString().slice(0, -1));
    } else {
      current.value = eval(result.value);
    }
  }
}
</script>

<template>
  <div
    class="w-1/2 calculator bg-slate-900 p-8 rounded-xl text-white container grid grid-cols-5 gap-6 m-auto text-center  mt-16"
  >
    <div class="col-span-5 rounded">
      <div class="h-9 bg-green-700">{{ result }}</div>
      <div class="bg-red-400 h-5">{{ current }}</div>
    </div>
    <div @click="appendnum('7')"><button>7</button></div>
    <div @click="appendnum('8')"><button>8</button></div>
    <div @click="appendnum('9')"><button>9</button></div>
    <div
      @click="appendOperation('-')"
      class="bg-yellow-600 p-2 md:p-1 text-center rounded-full"
    >
      <button>-</button>
    </div>
    <div
      @click="appendOperation('/')"
      class="bg-yellow-600 p-2  md:p-1 text-center rounded-full"
    >
      <button>/</button>
    </div>
    <div @click="appendnum('4')"><button>4</button></div>
    <div @click="appendnum('5')"><button>5</button></div>
    <div @click="appendnum('6')"><button>6</button></div>
    <div
      @click="appendOperation('+')"
      class="row-span-2 bg-yellow-600 p-3  md:p-4 md:text-center rounded-full"
    >
      <button>+</button>
    </div>
    <div
      @click="appendOperation('*')"
      class="row-span-2 bg-yellow-600 p-3 ml-1 md:p-4 md:text-center rounded-full"
    >
      <button>x</button>
    </div>
    <div @click="appendnum('1')"><button>1</button></div>
    <div @click="appendnum('2')"><button>2</button></div>
    <div @click="appendnum('3')"><button>3</button></div>
    <div @click="appendnum('0')"><button>0</button></div>
    <div @click="appendnum('.')"><button>.</button></div>
    <div @click="clear"><button>C</button></div>
    <div @click="evaluate()" class="bg-red-500 rounded-full w-4  md:w-full">
      <button>=</button>
    </div>

    <div @click="removeLastCharCalculations" class="bg-red-500 rounded-full w-4 md:w-full">
      <button>E</button>
    </div>
  </div>
</template>

<style scoped>
.read-the-docs {
  color: #888;
}

.calculator div:hover {
  background-color: rgb(161, 103, 103);
  border-radius: 5px;
}
</style>
