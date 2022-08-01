<script setup>

    import { ref, computed } from 'vue';
    // Create a simple calculator component showing buttons
    // for adding, subtracting, multiplying and dividing.
    // It should also display the current result.
    // And show button for 0 - 9.
    // The calculator should also be able to handle negative numbers.
    // The calculator should also be able to handle decimal numbers.

    // The calculator component.
    const currentExpression = ref('');

    // The calculation result.
    const result = computed(() => {
        try {
            const value = parseFloat( eval( currentExpression.value ) );
            return value ? value : '0';
        } catch (e) {
            return '';
        }
    });

    // Adds a number to the current expression.
    function addNumber(number) {
        currentExpression.value += number;
    }

    // Removes the last number from the current expression.
    function removeLastNumber() {
        currentExpression.value = currentExpression.value.slice(0, -1);
    }

    // Clears the current expression.
    function clear() {
        currentExpression.value = '';
    }

    // Whether we're on the left bracket.
    const isLeftBracket = ref( true );

    // Handles the bracket button.
    function handleBracket() {
        currentExpression.value += isLeftBracket.value ? '(' : ')';
        isLeftBracket.value = ! isLeftBracket.value;
    }

</script>

<template>
    <div class="calculator">
        <div class="display">
            <div class="expression">{{ currentExpression }}</div>
            <div class="result">{{ result }}</div>
        </div>
        <div class="buttons">

            <!-- First row -->
            <div class="row">
                <button @click="clear()">C</button>
                <button @click="handleBracket()">
                    <span v-if="isLeftBracket">(</span>
                    <span v-else>)</span>
                </button>
                <button @click="addNumber('%')">%</button>
                <button @click="addNumber('/')">/</button>
            </div>
            
            <!-- Second row -->
            <div class="row">
                <button @click="addNumber('7')">7</button>
                <button @click="addNumber('8')">8</button>
                <button @click="addNumber('9')">9</button>
                <button @click="addNumber('*')">*</button>
            </div>

            <!-- Third row -->
            <div class="row">
                <button @click="addNumber('4')">4</button>
                <button @click="addNumber('5')">5</button>
                <button @click="addNumber('6')">6</button>
                <button @click="addNumber('-')">-</button>
            </div>

            <!-- Fourth row -->
            <div class="row">
                <button @click="addNumber('1')">1</button>
                <button @click="addNumber('2')">2</button>
                <button @click="addNumber('3')">3</button>
                <button @click="addNumber('+')">+</button>
            </div>

            <!-- Fifth row -->
            <div class="row">
                <button @click="addNumber('**')">^</button>
                <button @click="addNumber('0')">0</button>
                <button @click="addNumber('.')">.</button>
                <button @click="removeLastNumber()">D</button>
            </div>

        </div>
    </div>
</template>

<style scoped>
    .calculator {
        background: linear-gradient(to bottom, #fff, rgb(243, 55, 22) );
        max-width: 300px;
        width: 100%;
        height: auto;
        padding: 8px;
    }

    .display {
        text-align: right;
        padding: 20px;
        font-size: 20px;
        font-weight: 900;
        color: #fff;
        background-color: rgb(243, 55, 22);
        border-top-left-radius: 10px;
        border-top-right-radius: 10px;
        min-height: 100px;
        display: flex;
        flex-direction: column;
        justify-content: space-between;
    }

    .expression {
        font-size: 1.5em;
        min-height: 32px;
    }

    .buttons {
      	background-color: #fff;
    		margin-top: 0;
    }

    .row {
        display: flex;
        justify-content: space-between;
        padding: 20px;
    }

    button {
        display: flex;
        justify-content: center;
        align-items: center;
        text-align: center;
        background-color: rgb(225, 227, 228);
        width: 40px;
        height: 40px;
        border-radius: 50%;
        font-size: 28px;
        cursor: pointer;
        color: inherit;
        border: none;
    }
 
    button:last-child {
        color: #fff;
        background-color: rgb(243, 55, 22);
    }

</style>
