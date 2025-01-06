<script setup>
import { ref } from 'vue';
import { create, all } from 'mathjs'

const config = {}
const math = create(all, config)

const displayUpper = ref("");
const displayLower = ref("0");

const calculated = ref("");

function reset() {
    displayLower.value = "0";
    displayUpper.value = ""
    calculated.value = "";
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
    if (calculated.value.length > 0) {
        displayUpper.value = calculated.value;
    }
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

    let operandCount = 0;
    let numberCount = 0;


    // 1. Split original string 
    let splitString = displayUpper.value.split('');
    /*  2 Find if string contains: )
        a. only one or more operand -> return "NAN"
        b. only one or more number -> return number
        c. one or more operand but only one number -> return number
        d. Starts with an operand and is longer than 1? -> remove front operand
    */

    splitString.forEach(item => {
        item.match(/\D/) ? operandCount++ : "";
        item.match(/\d/) ? numberCount++ : "";
    })

    // Testing for base cases
    if ((originalString.length == operandCount) && numberCount == 0) {
        displayLower.value = "NAN";
    } if (originalString.length == numberCount) {
        console.log("One number")
    } if ((operandCount == originalString.length - 1) && numberCount == 1) {
        console.log("Case: one or more operand but only one number")
    } if (originalString.match(/^\D/) && originalString.length > 1) {
        console.log(splitString.slice(1).join(""))
    } if(originalString.match(/\.{2}/)) {
        console.log()
    }

    displayLower.value = math.evaluate(displayUpper.value);
    displayUpper.value = displayUpper.value + "=" + math.evaluate(displayUpper.value);
    calculated.value = math.evaluate(displayUpper.value);
}

</script>

<template>
    <div class="calculator">
        <div id="display" class="display">
            <div class="display__upper">
                {{ displayUpper }}
            </div>
            <div class="display__inner">
                {{ displayLower }}
            </div>
        </div>
        <button id="clear" class="btnAction btnAction--AC" @click="clickHandler">AC</button>
        <button id="divide" class="btnAction btnAction--divide" @click="clickHandler">/</button>
        <button id="multiply" class="btnAction btnAction--multiply" @click="clickHandler">*</button>
        <button id="subtract" class="btnAction btnAction--minus" @click="clickHandler">-</button>
        <button id="add" class="btnAction btnAction--plus" @click="clickHandler">+</button>
        <button id="equals" class="btnAction btnAction--enter" @click="calculate">=</button>
        <button id="decimal" class="btnDigit btnDigit--dot" @click="clickHandler">.</button>
        <button id="0" class="btnDigit btnDigit--0" @click="clickHandler">0</button>
        <button id="1" class="btnDigit btnDigit--1" @click="clickHandler">1</button>
        <button id="2" class="btnDigit btnDigit--2" @click="clickHandler">2</button>
        <button id="3" class="btnDigit btnDigit--3" @click="clickHandler">3</button>
        <button id="4" class="btnDigit btnDigit--4" @click="clickHandler">4</button>
        <button id="5" class="btnDigit btnDigit--5" @click="clickHandler">5</button>
        <button id="6" class="btnDigit btnDigit--6" @click="clickHandler">6</button>
        <button id="7" class="btnDigit btnDigit--7" @click="clickHandler">7</button>
        <button id="8" class="btnDigit btnDigit--8" @click="clickHandler">8</button>
        <button id="9" class="btnDigit btnDigit--9" @click="clickHandler">9</button>
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

/* -------------------------------------------------------------------------- */
/*                                   Buttons                                  */
/* -------------------------------------------------------------------------- */

button {
    cursor: pointer;
}

.btnDigit {
    background-color: #b7b7c0;
}

.btnDigit:hover {
    background-color: #a3a3ac;
}

.btnAction--AC {
    background-color: #C08BA6;
}

.btnAction--AC:hover {
    background-color: #a2748c;
}

.btnAction--enter {
    background-color: #8BA6C0;
}

.btnAction--enter:hover {
    background-color: #7a92a9;
}

/* ---------------------------------- Areas --------------------------------- */

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