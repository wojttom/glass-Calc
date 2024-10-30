<template>
    <div class="center">
        <div class="main">
            <div class="results" id="results">{{display}}</div>
            <div class="button number" id="copy" >Copy</div>
            <div class="button percent" @click ="percent" id="percent">%</div>
            <div class="button CE"@click ="clearEntry" id="CE">CE</div>
            <div class="button C" @click ="clear" id="C">C</div>
            <div class="button delete" @click="backspace" id="delete"><</div>
            <div class="button oneByX" @click ="invert"id="oneByX"><sup>1&nbsp;</sup>&frasl;<sub>&nbsp;x</sub></div>
            <div class="button square" @click="square"id="square">X<sup>2</sup></div>
            <div class="button root" @click ="sqrt"id="root"> √x</div>
            <div class="button divide" @click="setOperation('/')" id="divide">/</div>
            <div class="button number" @click="getNumber('7')" id="seven">7</div>
            <div class="button number" @click="getNumber('8')" id="eight">8</div>
            <div class="button number" @click="getNumber('9')" id="nine">9</div>
            <div class="button times" @click="setOperation('*')" id="times">*</div>
            <div class="button number" @click="getNumber('4')" id="four">4</div>
            <div class="button number" @click="getNumber('5')" id="five">5</div>
            <div class="button number" @click="getNumber('6')" id="six">6</div>
            <div class="button minus" @click="setOperation('=')" id="minus">-</div>
            <div class="button number" @click="getNumber('1')"id="one">1</div>
            <div class="button number" @click="getNumber('2')"id="two">2</div>
            <div class="button number" @click="getNumber('3')" id="three">3</div>
            <div class="button plus" @click="setOperation('+')" id="plus">+</div>
            <div class="button number zero" @click="getNumber('0')" id="zero">0</div>
            <div class="button coma" @click="getDecimal" id="coma">.</div>
            <div class="button equals" @click="calculate"id="equals">=</div>
        </div>
    </div>
</template>
<script lang="ts" setup>
    import { ref } from 'vue';
    const display = ref<string>('0')
    const currentNumber = ref<number | null>(null)
    const pendingNumber = ref<number | null>(null)
    const currentOperation =ref<string | null>(null)
    const isNewInput = ref<boolean>(true)

    //what the fuck
    function parser(str:string){
        return parseFloat(str)
    }

    const getNumber = (number: string) => {
        if(isNewInput.value){
            display.value=number
            isNewInput.value = false
        }else{
            display.value === '0' ? (display.value = number) : (display.value +=number)
        }
    }
    const getDecimal = () =>{
        if (isNewInput.value) {
            display.value = '0.'
            isNewInput.value = false
        }
        else if(!display.value.includes('.')){
            display.value+='.'
        }
    }
    const clear = () =>{
        display.value ='0'
        currentNumber.value=null
        currentOperation.value=null
        pendingNumber.value = null
        isNewInput.value = true;
    }
    const clearEntry = () =>{
        display.value='0'
        isNewInput.value = true
    }
    const backspace = () => {
        display.value.length>1? display.value = display.value.slice(0,-1) : display.value = '0'
    }
    const invert = () =>{
        const currentValue = parseFloat(display.value)
        currentValue !==0 ? display.value = (1/currentValue).toString() : display.value = 'Błąd'
    }
    const square = () =>{
        const currentValue = parseFloat(display.value)
        display.value = (currentValue ** 2).toString()
    }
    const sqrt = () =>{
        const currentValue = parseFloat(display.value)
        display.value = currentValue >= 0 ? Math.sqrt(currentValue).toString() : 'Błąd'
    }
    const percent = () =>{
        const currentValue = parseFloat(display.value)
        display.value = (currentValue/100).toString()
    }
    const setOperation = (operation: string) =>{
        if(currentOperation.value && !isNewInput.value){
            calculate()
        }else{
            currentNumber.value = parseFloat(display.value)
        }
        currentOperation.value = operation;
        isNewInput.value = true;
    }

    const calculate = () =>{
        const secondNumber = parseFloat(display.value)
        if(currentOperation.value && currentNumber.value !==null){
            let results:number | string = 0
            switch(currentOperation.value){
                case '+':
                    results=currentNumber.value + secondNumber
                    break
                case '-':
                    results=currentNumber.value - secondNumber
                    break
                case '*':
                    results=currentNumber.value * secondNumber
                    break
                case '/':
                    results= secondNumber===0 ? 'Dzielenie przez 0 niedozwolone' : currentNumber.value / secondNumber
                    break
            }
            display.value = results.toString()
            currentNumber.value = typeof results === 'number' ? results : 0
            pendingNumber.value = secondNumber
            isNewInput.value = true
        }else if(pendingNumber.value !== null && currentOperation.value){
            if(currentNumber.value !== null && pendingNumber.value !== null){
                const result = operate(currentNumber.value!, pendingNumber.value!, currentOperation.value!)
                display.value = result!.toString()
                currentNumber.value = typeof result === 'number' ? result : 0
            }
        }
    }
    const operate = (first:number, second:number, operation:string) => {
            switch(operation){
                case '+':
                    return first + second
                case '-':
                    return first - second
                case '*':
                    return first * second
                case '/':
                    return second===0 ? 'Dzielenie przez 0 niedozwolone' : first / second
                default:
                    first
            }
        }
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Rubik:ital,wght@0,300..900;1,300..900&display=swap');

*{
    font-family:Rubik;
    color:white;
    font-size:40px;
    user-select: none;
}
body{
    margin:0;
    padding:0;
}
.center{
    display:flex;
    align-items:center;
    justify-content:center;
}
.main{
    position:absolute;
    top:4%;
    width:92%;
    max-width:1000px;
    min-width:380px;
    background: linear-gradient(135deg, rgba(255,255,255,0.0), rgba(255,255,255,0.2));
    backdrop-filter:blur(5px);
    -webkit-backdrop-filter:blur(5px);
    height:800px;
    border:1px solid white;
    border-radius: 24px;
    display:grid;
    grid-template-columns: repeat(4, 1fr);
    grid-template-rows: repeat(7, 1fr);
    grid-gap: 4px 4px;
}
.button, .results{
    margin:8px;
    background: linear-gradient(125deg, rgba(255, 255, 255, 0.341), rgba(255,255,255,0));
    backdrop-filter:blur(10px);
    -webkit-backdrop-filter:blur(10px);
    border-radius: 24px;
    border:2px solid rgba(255,255,255,0.3);
    box-shadow: 0 8px 32px 0 rgba(0,0,0,0.2);
    display: flex;
    align-items: center;
    justify-content: center;
    text-shadow: 0px 0 20px black;
    transition: 0.2s linear;
}
.results{
    grid-column: 1 / 4;
    justify-content: start;
    position: relative;
    padding-left: 20px;
}
.button.zero{
    grid-column: 1 / 3;
}
.number{
    background: linear-gradient(45deg, rgba(54, 66, 61, 0.449), rgba(135, 135, 134, 0.48));
}
.button:hover{
    background: rgba(117, 117, 117, 0.545)
}
.button:active{
    transition: 0.2s cubic-bezier(0.075, 0.82, 0.165, 1);
    transform: scale(0.9);
    font-size: 110%;
}
.equals{
    background: linear-gradient(45deg, #00f72977, #abd3b193);
}
.equals:hover{
    background: linear-gradient(45deg, #00a81c77, #6f897393);
}

</style>