<template>
    <div>
        <MessagePedido :msg="msg" v-show="msg"/>
        <div>
            <form id="form-container" @submit="createBurger">
                <div class="input-container">
                    <label for="nome">Nome do cliente:</label>
                    <input type="text" name="nome" id="nome" v-model="nome" placeholder="Informe seu nome">
                </div>

                <div class="input-container">
                    <label for="pao">Escolha o tipo de pão</label>
                    <select name="pao" id="pao" v-model="pao">
                        <option value="" selected>Selecione o tipo de pao</option>
                        <option v-for="pao in paes" :key="pao.id" :value="pao.tipo">{{ pao.tipo }}</option>
                    </select>
                </div>

                <div class="input-container">
                    <label for="carne">Escolha o tipo de carne</label>
                    <select name="carne" id="carne" v-model="carne">
                        <option value="" selected>Selecione o tipo de carne</option>
                        <option v-for="carne in carnes" :key="carne.id" :value="carne.tipo">{{ carne.tipo }}</option>
                    </select>
                </div>

                <div class="input-container" id="opcionais-container">
                    <label for="opcionais">Selecione os opcionais:</label>
                    <div class="checkbox-container" v-for="opcional in opcionaisdata" :key="opcional.id">
                        <input type="checkbox" name="opcionais" v-model="opcionais" :value="opcional.tipo"><span>{{opcional.tipo}}</span>
                    </div>
                </div>

                <div class="input-container">
                    <input type="submit" class="submit-btn" value="Criar Burger">
                </div>
            </form>
        </div>
    </div>
</template>

<script>
    import MessagePedido from "./Message.vue"

    export default {
        name: "BurgerForm",
        data() {
            return {
                //request
                paes: null,
                carnes: null,
                opcionaisdata: null,
                //response
                nome: null,
                pao: null,
                carne: null,
                opcionais: [],
                msg: null
            }
        },
       methods: {
            async getIngredientes() {
                const req = await fetch('http://localhost:3000/ingredientes')
                const data = await req.json()

                this.paes = data.paes
                this.carnes = data.carnes
                this.opcionaisdata = data.opcionais
            },
            async createBurger(e) {
                e.preventDefault()

                const pedido = {
                    nome: this.nome,
                    pao: this.pao,
                    carne: this.carne,
                    opcionais: Array.from(this.opcionais),
                    status: "Solicitado",
                }

                const pedidoJson = JSON.stringify(pedido)

                const req = await fetch('http://localhost:3000/burgers', {
                    method: "POST",
                    headers: {"Content-Type": "application/json"},
                    body: pedidoJson
                })

                const res = await req.json()

                //Adicionar msg
                this.msg = `Pedido N° ${res.id} realizado com sucesso`

                //Limpar msg
                setTimeout(() => this.msg = "" , 2500)

                //Limpar campos
                this.nome = ""
                this.pao = ""
                this.carne = ""
                this.opcionais = []
            }
        },
        mounted() {
            this.getIngredientes()
        },
        components: {
            MessagePedido
        }
    }
</script>

<style scoped>
    #form-container {
        max-width: 400px;
        margin: 0 auto;
    }

    .input-container {
        display: flex;
        flex-direction: column;
        margin-bottom: 20px;
    }

    label {
        font-weight: bold;
        margin-bottom: 15px;
        color: #222;;
        padding: 5px 10px;
        border-left: 4px solid #fcba03;
    }

    input, select {
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
        margin-top: -3px;
        margin-left: 6px;
        font-weight: bold;
    }

    .submit-btn {
        background-color: #222;
        color:#fcba03;
        font-weight: bold;
        border: 2px solid #222;
        padding: 10px;
        font-size: 16px;
        margin: 0 auto;
        cursor: pointer;
        transition: .5s;
    }

    .submit-btn:hover {
        background-color: transparent;
        color: #222;
    }
</style>