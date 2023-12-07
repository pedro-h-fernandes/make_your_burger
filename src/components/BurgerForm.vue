<template>
    <Messages :msg="msg" v-show="msg" />
    <form id="burger-form" @submit="criarBurger">
        <div class="mb-3">
            <label for="nomeCliente" class="form-label">Nome do cliente:</label>
            <input required type="text" class="form-control h-auto border border-black" id="nome" name="nome" v-model="nome"
                placeholder="Digite seu nome">
        </div>

        <div class="mb-3">
            <label for="pao">Escolha o tipo de pão:</label>
            <select required class="form-select h-auto border border-black" name="pao" id="pao" v-model="pao">
                <option value="">Selecione o seu pão</option>
                <option v-for="(pao, index) in paes" :key="index" :value="pao.tipo">{{ pao.tipo }}</option>
            </select>
        </div>

        <div class="mb-3">
            <label for="carne">Escolha a carne do seu burger:</label>
            <select required class="form-select h-auto border border-black" name="carne" id="carne" v-model="carne">
                <option value="">Selecione o tipo de carne</option>
                <option v-for="(carne, index) in carnes" :key="index" :value="carne.tipo">{{ carne.tipo }}</option>
            </select>
        </div>

        <div id="opcionais-container" class="input-container">
            <label id="opcionais-title" for="opcionais">Selecione os opcionais:</label>
            <div v-for="opcional in opcionaisData" :key="opcional.id" class="checkbox-container mb-3 ">
                <input type="checkbox" name="opcionais" id="opcionais" v-model="opcionaisCli" :value="opcional.tipo">
                <span> {{ opcional.tipo }}</span>
            </div>
        </div>

        <div class="input-btn">
            <input type="submit" class="submit-btn h-auto" value="Criar meu burger">
        </div>
    </form>
</template>

<script setup>
import Messages from './Messages.vue';
import { ref, onMounted } from 'vue';

const paes = ref(null);
const carnes = ref(null);
const opcionaisData = ref(null);
const nome = ref(null);
const pao = ref(null);
const carne = ref(null);
const opcionaisCli = ref([]);
const msg = ref(null);

const getIngredients = async () => {
    const req = await fetch('http://localhost:3000/ingredientes');
    const data = await req.json();
    paes.value = data.paes;
    carnes.value = data.carnes;
    opcionaisData.value = data.opcionais;
};

const criarBurger = async (e) => {
    e.preventDefault();
    const data = {
        nome: nome.value,
        carne: carne.value,
        pao: pao.value,
        opcionais: Array.from(opcionaisCli.value),
        status: 'Solicitado'
    };

    const dataJson = JSON.stringify(data);
    const req = await fetch('http://localhost:3000/pedidos', {
        method: 'POST',
        headers: { "Content-Type": "application/json" },
        body: dataJson,
    });

    const res = await req.json();

    msg.value = `Hamburger Nº ${res.id} realizado com sucesso`;

    setTimeout(() => {
        msg.value = "";
    }, 3000);

    limparCampos();
};

const limparCampos = () => {
    nome.value = '';
    carne.value = '';
    pao.value = '';
    opcionaisCli.value = [];
};

onMounted(() => {
    getIngredients();
});
</script>
<style scoped>
#burger-form {
    width: 100%;
    font-size: 3vw;
}

.input-container {
    display: flex;
    flex-direction: column;
    margin-bottom: 20px;
}

label {
    font-weight: bold;
    font-size: 1.4vw;
    margin-bottom: 10px;
    color: #222;
    padding: 5px 10px;
    border-left: 4px solid #fcba03;
}

input,
select {
    padding: 6px 10px;
    font-size: 1.6rem;
    width: 30vw;
    height: 4vh;
}

input::placeholder {
    font-size: 1.2vw;
}

#opcionais-container {
    flex-direction: row;
    flex-wrap: wrap;
    width: 30vw;
}

#opcionais-title {
    width: 100%;
}

.checkbox-container {
    display: flex;
    align-items: center;
    width: 50%;
    margin-bottom: 20px;
}

option {
    font-size: 1vw;
}

.checkbox-container input {
    width: 0.7vw;
}

.checkbox-container span {
    margin-left: 6px;
    font-weight: bold;
    font-size: 1vw;
}

.input-btn {
    width: fit-content;
}

.submit-btn {
    background-color: #222;
    color: #fcba03;
    height: 6vh;
    font-size: 1.15vw;
    font-weight: bold;
    border: 2px solid #222;
    cursor: pointer;
    transition: .5s;
    box-shadow: 2px 2px 4px #000000c0;
}

.submit-btn:hover {
    background-color: transparent;
    color: #222;
}


@media screen and (min-width: 320px) and (max-width: 768px) {
    label {
        font-size: 3vw;
    }

    option {
        font-size: 2vw;
    }

    .submit-btn {
        font-size: larger;
    }

    input,
    select,
    .input-container {
        width: 80vw;
    }

    input::placeholder {
        font-size: 3vw;
    }

    .checkbox-container input {
        width: 3vw;
    }

    .checkbox-container span {
        font-size: 3vw;
    }

    #opcionais-container {
        width: 80vw;
    }
}
</style>