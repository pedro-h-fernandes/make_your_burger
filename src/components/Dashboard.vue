<template>
    <Messages :msg="msg" v-show="msg" />
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
                            <select name="status" class="status" @change="updateBurger($event, pedido.id)">
                                <option value="">Selecione</option>
                                <option v-for="status in status" :key="status.id" :selected="pedido.status == status.tipo"
                                    :value="status.tipo">{{ status.tipo }}
                                </option>
                            </select>
                            <button class="delete-btn" @click="deleteBurger(pedido.id)">
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
import Messages from './Messages.vue'
export default {
    name: 'Dashboard',

    data() {
        return {
            pedidos: null,
            msg: null,
            status: null
        }
    },

    components: {
        Messages,
    },

    methods: {
        async getPedidos() {

            const req = await fetch('http://localhost:3000/pedidos')
            const data = await req.json()

            this.pedidos = data;
        },

        async getStatus() {
            const req = await fetch('http://localhost:3000/status')
            const data = await req.json()

            this.status = data;
        },

        async deleteBurger(id) {
            const req = await fetch(`http://localhost:3000/pedidos/${id}`, {
                method: "DELETE" //este modo de fazer funciona por conta da lib json serve onde esta sendo feito o bakend
            })

            const res = await req.json()
            //msg
            this.msg = `Hamburger removido com sucesso`

            this.limpaMsgApos3Seg()

            this.getPedidos()
        },

        async updateBurger(event, id) {
            const option = event.target.value;
            const dataJson = JSON.stringify({ status: option })
            const req = await fetch(`http://localhost:3000/pedidos/${id}`, {
                method: "PATCH",
                headers: { "Content-Type": "application/json" },
                body: dataJson,
            })
            
            const res = await req.json();
            this.msg = `Hamburger Nº ${res.id} atualizado com sucesso para "${res.status}"`
            this.limpaMsgApos3Seg()
            console.log(res)
        },

        limpaMsgApos3Seg() {
            setTimeout(() => this.msg = "", 3000)
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
    font-size: 1.6rem;

}

thead th,
tbody td {
    max-width: 90px;
}

tbody td {
    border: 1px solid black;
    padding-left: 5px;
    font-size: 1.6rem;
}

.opcionais ul {
    margin-left: 20px;
    font-size: 2.5rem;
    padding: 2px;
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
    width: 55%;
    height: 25px;
    font-size: 1.5rem;
}

select option {
    font-size: 1.2rem;
}

.delete-btn {
    background-color: transparent;
    border-radius: 5px;
    padding: 2px;
    border: 1px solid #000000;
    transition: .5s;
    font-size: 2rem;
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