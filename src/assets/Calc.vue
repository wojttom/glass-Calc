<template>
    <div class="center">
        <div class="main">
            <div class="results" id="results">{{display}}</div>
            <div class="button number" id="copy" >Copy</div>
            <div class="button percent" id="percent">%</div>
            <div class="button CE" id="CE">CE</div>
            <div class="button C" @click ="" id="C">C</div>
            <div class="button delete" @click="" id="delete"><</div>
            <div class="button oneByX" id="oneByX"><sup>1&nbsp;</sup>&frasl;<sub>&nbsp;x</sub></div>
            <div class="button square" @click=""id="square">X<sup>2</sup></div>
            <div class="button root" id="root"> √x</div>
            <div class="button divide" @click=""id="divide">/</div>
            <div class="button number" v-on:click="" id="seven">7</div>
            <div class="button number" @click="" id="eight">8</div>
            <div class="button number" @click="" id="nine">9</div>
            <div class="button times" @click=""id="times">*</div>
            <div class="button number" @click="" id="four">4</div>
            <div class="button number" @click="" id="five">5</div>
            <div class="button number" @click="" id="six">6</div>
            <div class="button minus" @click=""id="minus">-</div>
            <div class="button number" @click=""id="one">1</div>
            <div class="button number" @click=""id="two">2</div>
            <div class="button number" @click="" id="three">3</div>
            <div class="button plus" @click="" id="plus">+</div>
            <div class="button number zero" @click="" id="zero">0</div>
            <div class="button coma" @click="" id="coma">,</div>
            <div class="button equals" @click=""id="equals">=</div>
        </div>
    </div>
</template>
<script lang="ts">
import { ref } from 'vue';
    export default{
        setup(){

            // Definicja
            let display = ref('');
            let number1 = ref('');
            let number2 = ref('');
            let isEnteringNumber2 = ref(false);
            let operator = ref('');
            let results = 0;
            let numberTyped = ref("");
            const operators = ['+', '-', '*', '/'];

            // Logika
            // Wprowadzanie liczb

            // Obsługa przecinka 

            // Obsługa operatorów 
            
            // Czyszczenie wszystkiego 
            // NIE DZIAŁA W 100%

            // Czyszczenie ostatniej liczby

            // Pierwiastek

            // Do potęgi 2

            // 1 przez liczbe wpisaną

            // Wykonywanie działań

            return {
                display,
            }
        },
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
.button.equals{
    background: linear-gradient(45deg, #00f72977, #abd3b193);
}
</style>