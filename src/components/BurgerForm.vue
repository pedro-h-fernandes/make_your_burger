<template>
    <div>
        <Messages :msg="msg" v-show="msg"/>
        <form id="burger-form" @submit="criarBurger">
            <div class="input-container">
                <label for="nomeCliente">Nome do cliente:</label>
                <input required type="text" id="nome" name="nome" v-model="nome" placeholder="Digite seu nome">
            </div>
            <div class="input-container">
                <label for="pao">Escolha o tipo de pão:</label>
                <select name="pao" id="pao" v-model="pao">
                    <option value="">Selecione o seu pão</option>
                    <option v-for="(pao, index) in paes" :key="index" :value="pao.tipo">{{ pao.tipo }}</option>
                </select>
            </div>
            <div class="input-container">
                <label for="carne">Escolha a carne do seu burger:</label>
                <select name="carne" id="carne" v-model="carne">
                    <option value="">Selecione o tipo de carne</option>
                    <option v-for="(carne, index) in carnes" :key="index" :value="carne.tipo">{{ carne.tipo }}</option>
                </select>
            </div>
            <div id="opcionais-container" class="input-container">
                <label id="opcionais-title" for="opcionais">Selecione os opcionais:</label>
                <div v-for="opcional in opcionaisData" :key="opcional.id" class="checkbox-container">
                    <input type="checkbox" name="opcionais" id="opcionais" v-model="opcionaisCli" :value="opcional.tipo">
                    <span> {{ opcional.tipo }}</span>
                </div>
            </div>

            <div class="input-btn">
                <input type="submit" class="submit-btn" value="Criar meu burger">
            </div>
        </form>
    </div>
</template>

<script>
import Messages from './Messages.vue'
export default {
    name: 'BurgerForm',

    components: {
        Messages
    },

    data() {
        return {
            paes: null,
            carnes: null,
            opcionaisData: null,

            nome: null,
            pao: null,
            carne: null,
            opcionaisCli: [],

            msg: null,
        }
    },

    methods: {
        async getIngredients() {
            const req = await fetch('http://localhost:3000/ingredientes')
            const data = await req.json()

            this.paes = data.paes;
            this.carnes = data.carnes;
            this.opcionaisData = data.opcionais
        },

        async criarBurger(e) {
            e.preventDefault();
            const data = {
                nome: this.nome,
                carne: this.carne,
                pao: this.pao,
                opcionais: Array.from(this.opcionaisCli),
                status: 'Solicitado'
            }

            const dataJson = JSON.stringify(data)
            const req = await fetch('http://localhost:3000/burgers', {
                method: 'POST',
                headers: { "Content-Type": "application/json" },
                body: dataJson,
            })

            const res = await req.json()

            this.msg = `Hamburger Nº ${res.id} realizado com sucesso`

            this.limpaMsgApos3Seg()
            this.limparCampos()
        },

        limparCampos() {
            this.nome = ''
            this.carne = ''
            this.pao = ''
            this.opcionaisCli = []
        },

        limpaMsgApos3Seg() {
            setTimeout(() => this.msg = "", 3000)
        }

    },

    mounted() {
        this.getIngredients()
    },

}
</script>
<style scoped>
#burger-form {
    max-width: 400px;
    margin: 0 auto;
    font-size: 5rem;
}

.input-container {
    display: flex;
    flex-direction: column;
    margin-bottom: 20px;
}

label {
    font-weight: bold;
    margin-bottom: 15px;
    color: #222;
    padding: 5px 10px;
    border-left: 4px solid #fcba03;
}

input,
select {
    padding: 5px 10px;
    width: 300px;
}

#opcionais-container {
    flex-direction: row;
    flex-wrap: wrap;
}

#opcionais-title {
    width: 100%;
}

.checkbox-container {
    display: flex;
    align-items: flex-start;
    width: 50%;
    margin-bottom: 20px;
}

.checkbox-container span,
.checkbox-container input {
    width: auto;
}


.checkbox-container span {
    margin-left: 6px;
    font-weight: bold;
    font-size: 1.5rem;
}

.input-btn {
    width: fit-content;
}

.submit-btn {
    background-color: #222;
    color: #fcba03;
    font-weight: bold;
    border: 2px solid #222;
    padding: 10px;
    margin: 0 auto;
    cursor: pointer;
    transition: .5s;
}

.submit-btn:hover {
    background-color: transparent;
    color: #222;
}
</style>