<template>
    <div class="calculator">
        <header class="title">Calculator</header>
        <div class="display">
            <h1 class="current"> {{ current || '0'}}</h1>
        </div>
        <div class="keyboard">
            <div @click="clear" class="operator clear" >C</div>
            <div @click="del" class="operator delete">DEL</div>
            <div @click="sign" class="operator">-/+</div>
            <div @click="percent" class="operator">%</div>
            <div @click="divide" class="operator">/</div>
            <div @click="times" class="operator">*</div>
            <div @click="append('7')" class="digit">7</div>
            <div @click="append('8')" class="digit">8</div>
            <div @click="append('9')" class="digit">9</div>
            <div @click="minus" class="operator">-</div>
            <div @click="append('4')" class="digit">4</div>
            <div @click="append('5')" class="digit">5</div>
            <div @click="append('6')" class="digit">6</div>
            <div @click="add" class="operator">+</div>
            <div @click="append('1')" class="digit">1</div>
            <div @click="append('2')" class="digit">2</div>
            <div @click="append('3')" class="digit">3</div>
            <div @click="append('0')" class="digit zero">0</div>
            <div @click="dote" class="digit">.</div>
            <div @click="equal" class="operator equal">=</div>
        </div>
    </div>

</template>

<script>
export default {
    data() {
        return {
            current: '',
            operator: null,
            previous: null,
            operatorClicked: false,
        }
    },
    methods: {
        clear() {
            this.current = ''
        },
        del() {
            this.current = this.current.substr(0, this.current.length - 1)
        },
        sign() {
            this.current = this.current.charAt(0) === '-' ? this.current.slice(1) : `-${this.current}`
        },
        percent() {
            this.current = `${parseFloat(this.current) / 100}`
        },
        append(number) {
            if(this.operatorClicked === true) {
                this.current = ''
                this.operatorClicked = false
            } 
            if(this.current.length <= 14) {
                this.current = `${this.current}${number}`
            }
        },
        dote() {
            if(this.current.indexOf('.') === -1) {
                this.append('.')
                if(this.current.indexOf('.') === 0) {
                    this.current = `0${this.current}`
                }
            }
        },
        setPrevious() {
            this.previous = this.current
            this.operatorClicked = true
        },
        divide() {
            this.operator = (a, b) => a / b
            this.setPrevious()
        },
        times() {
            this.operator = (a, b) => a * b
            this.setPrevious()
        },
        minus() {
            this.operator = (a, b) => a - b
            this.setPrevious()
        },
        add() {
            this.operator = (a, b) => a + b
            this.setPrevious()
        },
        equal() {
            this.current = `${this.operator(
                parseFloat(this.previous),
                parseFloat(this.current)
            )}`
            this.previous = null
        }
    }
}
</script>

<style scoped>
    .calculator{
        display: flex;
        flex-wrap: wrap;
        position: relative;
        width: 290px;
        min-height: 400px;
        height: 70%;
        background-color: #140633;
        
        font-family: 'Roboto', sans-serif;
        color: #fff;

        user-select: none;
    }

    .title {
        width: 100%;
        padding-top: 5px;
        justify-content: center;
        text-align: center;
        font-size: 10pt;
    }

    .display {
        display: flex;
        top: 0;
        width: 100%;
        min-height: 95px;
        max-height: 170px;
        
        align-items: flex-end;
        justify-content: flex-end;
        padding: 10px;
    }

    .display > h1 {
        box-sizing: border-box;
    }

    .keyboard {
        width: 95%;
        min-height: 250px;
        height: 305px;
        margin: 0 auto;
        padding-top: 5px;
        display: grid;
        grid-template-columns: repeat(4, 1fr);
        grid-template-rows: minmax(50px);
        grid-gap: 5px !important;
    }

    .digit, .operator {
        display: flex;
        justify-content: center;
        align-items: center;
        height: 100%;
        background-color: #B8A5D910;
    }

    .digit:hover {
        background-color: #B8A5D9;
        cursor: pointer;
    }

    .operator:hover {
        background-color: #A044D9;
        cursor: pointer;
    }

    .zero, .clear {
        grid-column-start: 1;
        grid-column-end: 3;
    }
    .delete {
        grid-column-start: 3;
        grid-column-end: 5;
    }

    .equal {
        background-color: #83C0B920;
        grid-column-start: 4;
        grid-column-end: 5;
        grid-row-start: 5;
        grid-row-end: 7;
    }

    .equal:hover {
        background-color: #83C0B9;
    }

</style>