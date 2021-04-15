<template>
  <q-page class="container">
    <div class="mobile">
      <div class="mobile__toolbar">Lançamentos</div>



      <div class="cooperado">
      <div class="cooperado__title">Seja bem-vindo, {{cooperado.nome}}</div>
        <span class="cooperado__saldo"> Saldo: R$ {{cooperado.saldo}}</span>

        <q-btn @click="atualizarSaldo" class="cooperado__atualizar-saldo" no-caps>Atualizar Saldo</q-btn>

        <div class="cooperado__lancamento">

          <q-select class="cooperado__select" v-model="cooperadoSelecionado" color="green" :options="cooperadosAmigos" outlined label="Cooperado" />

          <q-input label="Valor" v-model="valor" type="number" outlined></q-input>

          <q-btn @click="transferir" class="cooperado__atualizar-saldo" no-caps>Transferir</q-btn>
        </div>
      </div>
    </div>
  </q-page> 
</template>

<script>
import axios from 'app/node_modules/axios'
export default {
  name: 'PageIndex',
  data() {
    return {
      cooperadoSelecionado: null,
      cooperadosAmigos: [
        {
        label:"Felipe",
        value:2,
        }
      ],
      valor:0,
      cooperado: {
        id: 0,
        nome: '',
        saldo: 0, 
        conta: ''
      }
    }
  },

  mounted() {
    this.login();
    this.cooperadoSelecionado = this.cooperadosAmigos[0]
  },

  methods: {
    login() {
      this.cooperado.id = 1
      this.cooperado.nome = "Anderson"
      this.cooperado.conta = "0000110-7"
      this.cooperado.saldo = 800
    },

    atualizarSaldo() {
      this.cooperado.saldo = 800
    },

    transferir() {
    if(this.valor <= this.cooperado.saldo){
        this.cooperado.saldo -= this.valor 
    }
    }
  },
}
</script>

<style lang="scss">

  @import url('https://fonts.googleapis.com/css2?family=Quicksand:wght@300;400;500;600;700&display=swap');

  * {
    font-family: 'Quicksand', sans-serif;
  }

  .container {
    display: grid;
    justify-items: center;
    width: 100%;
    padding-top: 2.5rem;

  }

  .mobile {
    background: rgb(252, 247, 247);
    width: 20rem;

    &__toolbar {
      display: grid;
      align-items: center;
      font-size: 1.125rem;
      font-weight: 600;
      color: white;
      
      background: rgb(4, 77, 10);

      height: 64px;
      width: 100%;

      padding:8px 16px;
    }
  }

  .cooperado {
    display: grid;
    grid-gap: 1.25rem;
    width: 100%;
    padding: 16px;
    
    &__saldo {
      color: rgb(18, 41, 13);
      font-size: 1.125rem;
      font-weight: 700;
    }

    &__title {
      font-size: 1.125rem;
      font-weight: 600;
    }

    &__atualizar-saldo {
      background: rgb(4, 77, 10);
      color: white;
      width: 100%;

      font-size: 1.125rem;
      font-weight: 600;
    }

    &__select {
      font-size: 1.125rem;
      font-weight: 600;
    }

    &__lancamento {
      display: grid;
      grid-gap: 1.25rem
    }
  }


</style>
