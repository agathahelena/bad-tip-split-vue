<script setup>
import { ref } from 'vue';

const bill = ref('');
const tip = ref('');
const people = ref('');

const total = ref(0);
const tipValue = ref(0);
const perPerson = ref(0);
const message = ref('');
const messageType = ref('');
const showResult = ref(false);  // Controla se o resultado será mostrado

function calculate() {
    const billValue = Number(bill.value.replace(',', '.'));
    const tipPercent = Number(tip.value.replace(',', '.'));
    const peopleCount = Number(people.value);

    if (!billValue || !tipPercent || !peopleCount) {
        alert('Preencha os dados');
        message.value = 'Algo deu errado.';
        messageType.value = 'error';
        return;
    }

    tipValue.value = ((billValue * tipPercent) / 100).toFixed(2).replace('.', ',');
    total.value = (billValue + parseFloat(tipValue.value)).toFixed(2).replace('.', ',');
    perPerson.value = (parseFloat(total.value) / peopleCount).toFixed(2).replace('.', ',');
    message.value = 'Ok';
    messageType.value = 'success';
    showResult.value = true;
}
</script>

<template>
    <div class="app">

        <div class="layout">
            <div class="panel" v-if="!showResult">
                <h2>Entradas</h2>
                <input v-model="bill" class="input" placeholder="Valor*" />
                <input v-model="tip" class="input" placeholder="Porcentagem*" />
                <input v-model="people" class="input" placeholder="Pessoas*" />
                <button class="small-btn" @click="calculate">Calcular</button>
            </div>

             <div class="panel" v-if="showResult">
                <h2>Resultado</h2>
                <div class="result">Total: R$ {{ total }}</div>
                <div class="result">Gorjeta: R$ {{ tipValue }}</div>
                <div class="result">Por pessoa: R$ {{ perPerson }}</div>
               <div :class="['result', messageType]">{{ message }}</div>
            </div>
        </div>
    </div>
</template>

<style>
@media (max-width: 600px){
.panel h2 {
    font-size: 1.1rem;
    color: #0d712e;
    font-weight: bold;
}

.panel {
    padding: 20px;
    border: 2px solid #125527;
    border-radius: 4px;
    margin-bottom: 30px;
}

.input {
    display: block;
    width: 100%;
    padding: 10px;
    margin-bottom: 10px;
    border: 1px solid #125527;
    border-radius: 4px;
}

.small-btn{
    padding: 10px;
    color:#083015;
    border-radius: 4px;
    border: 1px solid #125527;
    cursor: pointer;
    background: #f7faf8;
    font-size: 0.875rem;
}
.result {
    font-size: 1rem;
}

.success {
    color: green;
    font-weight: bold;
}

.error {
    color: red;
    font-weight: bold;
}
}
</style>
