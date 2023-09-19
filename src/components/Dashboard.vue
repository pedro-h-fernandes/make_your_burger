<template>
    <div id="burgerTable">
        <table style="width:70%;">
            <thead>
                <tr>
                    <th class="order-id">#:</th>
                    <th>Cliente:</th>
                    <th>Pão:</th>
                    <th>Carne:</th>
                    <th>Opcionais:</th>
                    <th>Ações</th>
                </tr>
            </thead>

            <tbody>
                <tr class="burger-table-row" v-for="pedido in pedidos" :key="pedido.id">
                    <td class="order-number">{{ pedido.id }}</td>
                    <td>{{ pedido.nome }}</td>
                    <td>{{ pedido.pao }}</td>
                    <td>{{ pedido.carne }}</td>
                    <td class="opcionais">
                        <ul>
                            <li v-for="opcionais in pedido.opcionais">{{ opcionais }}</li>
                        </ul>
                    </td>
                    <td class="acoes">
                        <div>
                            <select name="status" class="status">
                                <option value="{{ pedido.status }}">{{ pedido.status }}</option>
                            </select>
                            <button class="delete-btn">
                                <div class="cancelar"><img src="/img/x-circle.svg" alt="">Cancelar</div>
                            </button>

                        </div>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
</template>
<script>
export default {
    name: 'Dashboard',

    data() {
        return {
            pedidos: null,
            status:null
        }
    },

    methods: {
        async getPedidos() {

            const req = await fetch('http://localhost:3000/burgers')
            const data = await req.json()

            console.log(data)
            this.pedidos = data;
        },

        async getStatus() {
            const req = await fetch('http://localhost:3000/status')
            const data = await req.json()

            console.log(data)
            this.status = data;
        }
    },

    mounted() {
        this.getPedidos();
        this.getStatus()
    }
}
</script>
<style scoped>
#burgerTable {
    display: flex;
    justify-content: center;
}

table {
    border-collapse: collapse;
    box-shadow: 1px 1px 2px #0000003f;
}

thead th {
    border: 1px solid black;
    background-color: #f7c334;
    text-align: justify;
    padding: 2px;

}

thead th,
tbody td {
    max-width: 90px;
}

tbody td {
    border: 1px solid black;
    padding-left: 5px;
}

.opcionais ul {
    margin-left: 20px;
}

.acoes {
    padding: 3px;
}

.acoes div {
    display: flex;
    justify-content: space-around;
    align-items: center;
}

.acoes select {
    width: 50%;
    height: 25px;
}

.delete-btn {
    background-color: transparent;
    border-radius: 5px;
    padding: 2px;
    border: 1px solid #000000;
    transition: .5s;
}

.delete-btn:hover {
    background-color: #e6e6e6d7;
}

.cancelar {
    display: flex;
    flex-direction: column;
    align-items: center;
}

.cancelar img {
    max-width: 30px;
}
</style>