<script setup>
import { ref } from 'vue';

const bill = ref('');
const tip = ref('');
const people = ref('');

const total = ref(0);
const tipValue = ref(0);
const perPerson = ref(0);
const message = ref('');

function calculate() {
    const billValue = Number(bill.value);
    const tipPercent = Number(tip.value);
    const peopleCount = Number(people.value);

    if (!billValue || !tipPercent || !peopleCount) {
        alert('Preencha os dados');
        message.value = 'Algo deu errado.';
        return;
    }

    tipValue.value = (billValue * tipPercent) / 100;
    total.value = billValue + tipValue.value;
    perPerson.value = total.value / peopleCount;
    message.value = 'Ok';
}
</script>

<template>
    <div class="app">

        <div class="layout">
            <div class="panel">
                <h2>Entradas</h2>
                <input v-model="bill" class="input" placeholder="Valor" />
                <input v-model="tip" class="input" placeholder="Porcentagem" />
                <input v-model="people" class="input" placeholder="Pessoas" />
                <button class="small-btn" @click="calculate">Calcular</button>
            </div>

            <div class="panel">
                <h2>Resultado</h2>
                <div class="result">Total: {{ total }}</div>
                <div class="result">Gorjeta: {{ tipValue }}</div>
                <div class="result">Por pessoa: {{ perPerson }}</div>
                <div class="result">{{ message }}</div>
            </div>
        </div>
    </div>
</template>

<style>
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
</style>
