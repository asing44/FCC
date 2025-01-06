<script setup>
import { ref } from 'vue';

const displayUpper = ref("");
const displayLower = ref("0");
// ?* Need to get rid of "0" after start®

function reset() {
    displayLower.value = "0";
    displayUpper.value = ""
}

let initDisplay = function() {
    let toggler = false;
    if (!toggler) {
        toggler = true;
        displayLower.value = ""
    }
};

function clickHandler(event) {
    displayLower.value = "0";
    initDisplay();
    if (displayUpper.value + event.target.innerText != 0) {
        displayUpper.value = displayUpper.value + event.target.innerText
        event.target.classList.contains('btnDigit') ? appendInput(event) : null
        event.target.classList.contains('btnAction--AC') ? reset() : null
    } if (event.target.innerText.match(/[./+=-]/g)) {
        displayLower.value = event.target.innerText;
    }
    else {
        null
    }
}

function appendInput(event) {
    displayLower.value += event.target.innerText;
}
// Calculates top row
function calculate() {
    let originalString = displayUpper.value;
    // 0. Split original string 
    let splitString = displayUpper.value.split('');
    console.log(splitString, originalString)
    /* 0a Find if string contains: )
        1. only one or more operand -> return "NAN"
        2. only one or more number -> return number
        3. one or more operand but only one number -> return number  
    */
    if (splitString.match(/\D+/)) {
        return "NAN"
    }
    originalString.match(/[/*+-]/g) ? console.log("yes") : console.log("no")
    // 0b Find if string
    // 1. Find '/' and '*' in string
    //  1b. If none, find '+' and '-'
    // 2. Find number before and after step 1 result. Record start position and length of match.
    // 3. Complete operation with step 2 result and step 1 result
    // 4. Replace original match from step 2 with result of step 3
    // 5. Repeat until length is 1
    // 6. Return answer and replace lower display with answer
}

</script>

<template>
    <div class="calculator">
        <div class="display">
            <div class="display__upper">
                {{ displayUpper }}
            </div>
            <div class="display__inner">
                {{ displayLower }}
            </div>
        </div>
        <button class="btnAction btnAction--AC" @click="clickHandler">AC</button>
        <button class="btnAction btnAction--divide" @click="clickHandler">/</button>
        <button class="btnAction btnAction--multiply" @click="clickHandler">x</button>
        <button class="btnAction btnAction--minus" @click="clickHandler">-</button>
        <button class="btnAction btnAction--plus" @click="clickHandler">+</button>
        <button class="btnAction btnAction--enter" @click="calculate">=</button>
        <button class="btnDigit btnDigit--dot" @click="clickHandler">.</button>
        <button class="btnDigit btnDigit--0" @click="clickHandler">0</button>
        <button class="btnDigit btnDigit--1" @click="clickHandler">1</button>
        <button class="btnDigit btnDigit--2" @click="clickHandler">2</button>
        <button class="btnDigit btnDigit--3" @click="clickHandler">3</button>
        <button class="btnDigit btnDigit--4" @click="clickHandler">4</button>
        <button class="btnDigit btnDigit--5" @click="clickHandler">5</button>
        <button class="btnDigit btnDigit--6" @click="clickHandler">6</button>
        <button class="btnDigit btnDigit--7" @click="clickHandler">7</button>
        <button class="btnDigit btnDigit--8" @click="clickHandler">8</button>
        <button class="btnDigit btnDigit--9" @click="clickHandler">9</button>
    </div>
</template>

<style scoped>

    .calculator {
        display: grid;
        height: clamp(350px, 45vh, 800px);
        width: clamp(200px, 35vw, 250px);
        outline: 1px solid #464F61;
        border: 2px solid #2E3440;
        background-color: #C2C2D7;
        grid-template-rows: repeat(6, 1fr);
        grid-template-areas: 
            "display display display display""AC AC divide multiply""seven eight nine minus""four five six plus""one two three enter""zero zero decimal enter";
    }

    .btnAction, .btnDigit {
        height: auto;
        border: 1px solid #2E3440;
    }

    /* --------------------------------- Display -------------------------------- */

    .display {
        grid-area: display;
        min-height: 4.25rem;
        background-color: #2E3440;
    }

    .display__inner, .display__upper {
        display: flex;
        height: 50%;
        justify-content: end;
        align-items: center;
        padding: 4px;
        font-family: monospace;
        font-size: 1.5rem;
    }

    .display__upper {
        color: #E9DAAA;
        font-size: 1.25rem;
    }

    /* --------------------------------- Buttons -------------------------------- */

    .btnAction--AC {
        grid-area: AC;
    }

    .btnAction--divide {
        grid-area: divide;
    }

    .btnAction--multiply {
        grid-area: multiply;
    }

    .btnAction--minus {
        grid-area: minus;
    }

    .btnAction--plus {
        grid-area: plus;
    }

    .btnAction--enter {
        grid-area: enter;
    }

    .btnDigit--7 {
        grid-area: seven;
    }

    .btnDigit--8 {
        grid-area: eight;
    }

    .btnDigit--9 {
        grid-area: nine;
    }

    .btnDigit--6 {
        grid-area: six;
    }

    .btnDigit--5 {
        grid-area: five;
    }
    
    .btnDigit--4 {
        grid-area: four;
    }

    .btnDigit--3 {
        grid-area: three;
    }

    .btnDigit--2 {
        grid-area: two;
    }

    .btnDigit--1 {
        grid-area: one;
    }

    .btnDigit--0 {
        grid-area: zero;
    }

    .btnDigit--dot {
        grid-area: decimal;
    }

</style>