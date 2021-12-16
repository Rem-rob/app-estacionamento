<template>
  <div id="carro-table">

<mensagem :msg="msg" v-show="msg" />

    <div>
      <div id="carro-table-heading">
        <div class="order-id">#:</div>
        <div>Nome da pessoa</div>
        <div>Nome do carro</div>
        <div>Placa do carro</div>
        <div>Horário de entrada</div>
        <div>Ações: </div>
      </div>
    </div>

    <div id="carro-table-rows">

          <div class="carro-table-row" v-for="carro in carros" :key="carro.id" >


              <div class="order-number"> {{ carro.id }}</div>
              <div> {{ carro.nome }} </div>
              <div> {{ carro.nomeCarro }} </div>
              <div> {{ carro.placaCarro }} </div>
              <div> {{ carro.hora }} </div>

              <div>
          <select name="status" class="status" @change="updateCarro($event, carro.id)">
            <option value="">Status carro</option>
             <option :value="statu.tipo" v-for="statu in status" :key="statu.id" :selected="carro.status == statu.tipo"> {{ statu.tipo }} </option>
                  </select>

          <button class="delete-btn" @click="deletarCarro(carro.id)"> Deletar</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>

import Mensagem from './Mensagem.vue';

export default {
  name: "Dashboard",

  data() {
    return {
      carros: null,
      carros_id: null,
      status: [],
      msg : null
    }
  },

  //components da mensagem

  components : {
      Mensagem
  },

  // Carregar os carros do arquivo db.json

  methods: {
    async getCadastros() {
      const req = await fetch("http://localhost:3000/carros");
      const data = await req.json();
      this.carros = data;

      this.getStatus();
    },
    async getStatus() {
      const req = await fetch("http://localhost:3000/status");
      const data = await req.json();
      this.status = data;
    },
async deletarCarro(id) {
    const req = await fetch(`http://localhost:3000/carros/${id}`, {
     method: "DELETE"  
    });

        const data = await req.json();

        // mensage de cadastro de carro
          this.msg=`Carro deletado com sucesso!`;

          // limpar de a mensagem após um tempo

          setTimeout(()=> this.msg = "", 3000)


        this.getCadastros();
},

// atualizando o status do carro

async updateCarro(event, id){
    const opcoes = event.target.value;
    const dataJson = JSON.stringify({ status: opcoes }); // pega o ID do STATUS e CARROS
    const req =  await fetch(`http://localhost:3000/carros/${id}`, {

        method:"PATCH",
        headers:{"content-type" : "application/json"},
        body: dataJson

    });

    const res = await req.json();

 // mensage de cadastro de carro
          this.msg=`Carro do ${res.nome} foi atualizado para ${res.status}. Obrigado!`;

          // limpar de a mensagem após um tempo

          setTimeout(()=> this.msg = "", 3000)

}

  },

  mounted() {
    this.getCadastros();
  },
};
</script>

<style scoped>
#carro-table {
  max-width: 1200px;
  margin: 0 auto;
}

#carro-table-heading,
#carro-table-rows,
.carro-table-row {
  display: flex;
  flex-wrap: wrap;
}

#carro-table-heading {
  font-weight: bold;
  padding: 12px;
  border-bottom: 3px solid rgba(53, 30, 180);
}

#carro-table-heading div,
.carro-table-row div {
  width: 19%;
}

.carro-table-row {
  width: 100%;
  padding: 12px;
  border-bottom: 1px solid rgba(53, 30, 180);
}

.carro-table-row .order-number {
  width: 5%;
}

select {
  padding: 10px 6px;
  margin-right: 12px;
}

.delete-btn {
  background-color: #3f7fbf;
  color: white;
  font-weight: bold;
  padding: 10px;
  font-size: 16px;
  border: 2px solid white;
  cursor: pointer;
  transition: 0.5s;
}

.delete-btn:hover {
  background-color: tomato;
  font-size: 18px;
}
</style>