<script setup>

import Button from '@/components/CalculatorButton.vue';
import CalculatorButton from '@/components/CalculatorButton.vue';
import { ref } from 'vue';

const numberKeys = Array.from({ length: 10 }, (_, i) => i).reverse();
const operationKeys = ['+', '-', '*', '/'];

const output = ref('0');

let inputs = [];

const handleNumberButtonClick = (button) => {
    output.value === '0' ? output.value = button.target.textContent : output.value += button.target.textContent;
};

const handleOperationButtonClick = (button) => {
    inputs.push(output.value);
    inputs.push(button.target.textContent);
    output.value = '0';
};

const handleClearButtonClick = () => {
    output.value = '0';
    clear();
};

const handleDeleteButtonClick = () => {
    output.value = String(output.value).slice(0, -1);
};

const handleEqualsButtonClick = () => {
    inputs.push(output.value);
    calculate();
};

const clear = () => {
    inputs.splice(0, inputs.length);
}

const calculate = () => {
    output.value = eval(inputs.join(''));
    clear();
};

</script>

<template>
    <div class="calculator-container">
        <div class="calculator-display">
            <input class="calculator-input" :placeholder="output" readonly type="text">
        </div>
        <div class="keyboard">
            <div class="operations-keyboard">
                <CalculatorButton v-for="key in operationKeys" :text="key" class="btn-secondary w-100"
                                  v-on:click="handleOperationButtonClick"></CalculatorButton>
            </div>
            <div class="numbers-keyboard">
                <CalculatorButton v-for="key in numberKeys" :class="{ 'full-width': key === 0 }" :text="key"
                                  class="btn-primary" v-on:click="handleNumberButtonClick"></CalculatorButton>
            </div>
            <div class="output-keyboard">
                <Button class="btn-secondary h-100" text="C" v-on:click="handleClearButtonClick"></Button>
                <Button class="btn-secondary h-100" text="DEL" v-on:click="handleDeleteButtonClick"></Button>
                <Button class="btn-secondary h-100" style="background-color: green;" text="="
                        v-on:click="handleEqualsButtonClick"></Button>
            </div>
        </div>
    </div>
</template>

<style scoped>

.w-100 {
    width: 100%;
}

.h-100 {
    height: 100%;
}

.calculator-container {
    min-width: 400px;
    min-height: 650px;
    background: #f2f2f2;
    display: grid;
    grid-template-rows: 150px 450px;
    padding: 10px;
    gap: 10px;
    border-radius: 10px;
}

.calculator-display {
    width: 100%;
    height: 100%;
}

.calculator-display input {
    width: 100%;
    height: 100%;
    font-size: 20pt;
    text-align: right;
    padding: 10px;
    border: none;
    outline: none;
    background: #f2f2f2;
    border-radius: 5px;
}

.keyboard {
    display: grid;
    grid-template-columns: 300px 100px;
    grid-template-rows: 100px 350px;
    grid-template-areas: "operations output" "numbers output";
    gap: 10px

}

.operations-keyboard {
    width: 100%;
    height: 100%;
    grid-area: operations;
    display: flex;
    gap: 3px;
}

.numbers-keyboard {
    width: 100%;
    height: 100%;
    grid-area: numbers;
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    direction: rtl;
    gap: 3px;
}

.output-keyboard {
    width: 100%;
    height: 100%;
    grid-area: output;
    display: flex;
    flex-direction: column;
    gap: 3px;
}

.full-width {
    grid-column: span 3;
}

</style>