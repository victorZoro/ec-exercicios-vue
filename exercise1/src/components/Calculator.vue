<script setup>

import Button from '@/components/Button.vue';

const numbers = Array.from({ length: 10 }, (_, i) => i).reverse();
const operations = ['+', '-', '*', '/'];

</script>

<template>
    <div class="calculator-container">
        <div class="calculator-display">
            <input class="calculator-input" placeholder="0" readonly type="text">
        </div>
        <div class="keyboard">
            <div class="operations-keyboard">
                <Button v-for="operation in operations" :text="operation" class="btn-secondary w-100"></Button>
            </div>
            <div class="numbers-keyboard">
                <Button v-for="number in numbers" :class="{ 'full-width': number === 0 }" :text="number"
                        class="btn-primary"></Button>
            </div>
            <div class="output-keyboard">
                <Button class="btn-secondary h-100" text="C"></Button>
                <Button class="btn-secondary h-100" text="DEL"></Button>
                <Button class="btn-secondary h-100" style="background-color: green;" text="="></Button>
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