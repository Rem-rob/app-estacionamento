<template>
  <div>

      <mensagem :msg="msg" v-show="msg" />

    <form id="carro-form" @submit='createCarro'>
      <div class="input-container">
        <label for="nome">Nome da Pessoa: </label>
        <input
          type="text"
          id="nome"
          v-model="nome"
          placeholder="Informe o seu nome: "/>
      </div>

      <div class="input-container">
        <label for="nomeCarro">Nome do carro: </label>
        <input
          type="text"
          id="nomeCarro"
          v-model="nomeCarro"
          placeholder="Informe o nome do carro: "/>
      </div>
      <div class="input-container">
        <label for="placaCarro">Placa do carro: </label>
        <input
          type="text"
          id="placaCarro"
          v-model="placaCarro"
          placeholder="Informe a placa do carro: "/>
      </div>
      <div class="input-container">
        <label for="hora">Horário de entrada: </label>
        <input
          type="text"
          id="hora"
          v-model="hora"
          placeholder="Informe o horário de entrada: "/>
      </div>
      <div class="input-container">
        
        <input
          type="submit"
          class="submit-btn"
          value="Cadastrar o carro"
          >
      </div>
    </form>
  </div>
</template>

<script>

import Mensagem from './Mensagem.vue';

export default {
  components: { Mensagem },
  name: "CarroForm",
  data() {
      return {
          nome: null,
          nomeCarro: null,
          placaCarro: null,
          hora: null,
          msg: null
      }
  },

  methods: {
      async createCarro (e) {
          e.preventDefault();
          // console.log ("Carro cadastrado com sucesso");

          const data = {
              nome: this.nome,
              nomeCarro: this.nomeCarro,
              placaCarro: this.placaCarro,
              hora: this.hora,
              status: "Solicitado",
          }

          //console.log(data);

          const dataJson = JSON.stringify(data);

          //Fazendo um POST

          const req = await fetch("http://localhost:3000/carros", {
              method: "POST",
              headers: {"Content-Type" : "application/json"},
              body: dataJson
          });

          const res = await req.json();

          console.log (res);
            // mensage de cadastro de carro
          this.msg='Carro cadastrado com sucesso. Obrigado!';

          // limpar de a mensagem após um tempo

          setTimeout(()=> this.msg = "", 3000)

          //limpar campos

          this.nome = "";
          this.nomeCarro = "";
          this.placaCarro = "";
          this.hora = ""; 


      }
  },

    components: {
        Mensagem
    } 

}
</script>

<style scoped>

#carro-form {
    max-width: 300px;
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
    color: #222;
    padding: 5px 10px;
    border-left: 4px solid #3f7fbf;

}

input {
    padding: 5px 10px;
    widows: 300px;
}

.submit-btn {
    background-color: #3f7fbf;
    color: white;
    font-weight:bold ;
    padding: 10px;
    font-size: 16px;
    border: 2px solid white;
    cursor: pointer;
    transition: .5s;

}

.submit-btn:hover {
    background-color: tomato;
    font-size: 18px;
}
</style>