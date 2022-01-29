<template>
  <div>
      <Menssagem :msg="msg" v-show="msg"/>
      <div>
        <form id="pedido-form" @submit="createPedido">
          <!-- Input de cliente -->
            <div class="input-container">
              <label for="nome">Nome do cliente:</label>
              <input type="text" id="nome" name="nome" v-model="nome" placeholder="digite seu nome">
            </div>
            <!--  -->
             <div class="input-container">
              <label for="nome">Numero da Mesa:</label>
              <input type="text" id="mesa" name="mesa" v-model="mesa" placeholder="digite o numero da mesa">
            </div>
            <!-- Select do produto -->
            <div class="input-container">
              <label for="produto">Escolhe ai, oq tu vai querer comer:</label>
              <select name="comer" id="comer" v-model="comer">
                <option value="">--- Churrasco na Brasa ---</option>
                <option v-for="comer in produto" :key="comer.id" :value="comer.tipo">
                    {{ comer.name }}   {{comer.preço}}
                </option>
              </select>
              <div>
              <input class="input-produto" type="number" name="quantidadeProduto" v-model="quantidadeProduto" >
              </div>
            </div>
            <div class="input-container">
               <label for="liquido">Escolhe ai, oq tu vai querer beber:</label>
              <select name="beber" id="beber" v-model="beber">
                <option value="">------ Beber ------</option>
                <option v-for="beber in this.liquido" :key="beber.id" :value="beber.tipo">
                    {{ beber.name }}  -  {{ beber.preço }}
                </option>
              </select>
              <input class="input-produto" type="number" name="quantidadeLiquido" v-model="quantidadeLiquido" >
            </div>
            <div class="input-container">
            </div>            
            <div class="input-container-submit">
              <input type="submit" class="submit-btn" value="Fazer bem rapido!">
            </div>
        </form>
      </div>
  </div>
</template>

<script>
import Menssagem from '../Menssagem.vue';
import { setTimeout } from 'timers';
export default {

    name: 'FormPedido',
    data() {
        return {
            mesa: null,
            quantidadeProduto: Number,
            quantidadeLiquido: Number,
            preço: null,
            nome: null,
            mesas: null,
            preços: [],
            status: "solicitado",
            msg: null,
            produto: this.produto,
            liquido: this.liquido
        }
    },
    methods: {
      // Pega os dados da tabela Produto
        async getTabelaProduto() {
            const req = await fetch("http://localhost:3000/TabelaProduto");
            const data = await req.json();
            this.mesas = data.mesa;
            this.produto = data.Comer;
            this.liquido = data.Beber;
        },
        // cria o pedido
        async createPedido(e){
          e.preventDefault();
          
          const data = {
            nome: this.nome,
            mesa: this.mesa,
            comer: this.produto,
            beber: this.liquido,
            quantidadeProduto: this.quantidadeProduto,
            quantidadeLiquido: this.quantidadeLiquido,
            status: "Solicitado"
          }   
          
          const dataJson = JSON.stringify(data);

          const req = await fetch("http://localhost:3000/TabelaPedidos",{
              method: 'POST',
              headers: {"Content-Type":"application/json"},
              body: dataJson
          });
          const res = await req.json();
      
          // menssagem de sistema
          this.msg = `Pedido de N° ${res.id} realizado com sucesso`
          setTimeout(()=> this.msg = "",3000); 
          // limpar os campos
          this.nome = "",
          this.quantidadeProduto= null,
          this.quantidadeLiquido= null,
          this.mesa= "",
          this.produtos="",
          this.liquidos= ""
        }
    },
    mounted() {
        this.getTabelaProduto()
    },
    components: {
      Menssagem
    }
}
</script>

<style scoped>
  #pedido-form {
      max-width: 400px;
      margin: 0 auto;
      padding: 10px;

  }

  .input-container {
      display: flex;
      flex-direction: column;
      margin-bottom: 20px;
  }

  label{
      font-weight: bold;
      margin-bottom: 15px;
      color: #222;
      padding: 5px 10px;
      border-left: 4px solid #FCBA03; 
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

  .checkbox-container span, .checkbox-container input{
      width: auto;
  }

  .checkbox-container span{
      margin-left: 6px;
      font-weight: bold;
  }

  .submit-btn {
      background-color: #222;
      color: #FCBA03;
      font-weight: bold;
      border: 2px solid;
      border-radius: 10px ;
      padding: 10px;
      font-size: 16px;
      margin: 0 auto;
      cursor: pointer;
      transition: .5s;
  }

  .submit-btn:hover {
      background-color: transparent;
      color:#222;
  }
  .input-produto{
    max-width: 70px ;
    flex-wrap: wrap;
    flex-direction:row;
    margin-top: 5px; 
  }
  select{
    max-width: 200px;
    flex-wrap:wrap;
    flex-direction: row;
  }
</style>
