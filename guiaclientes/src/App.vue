<template>
  <div id="app">
    <h1>Cadastro</h1>

<div class="buttons">
  <button class="button is-info">Info</button>
  <button class="button is-success">Success</button>
  <button class="button is-warning">Warning</button>
  <button class="button is-danger">Danger</button>
</div>

      <small id="nomeErro" v-show="deuErro">O nome é invalido, tente novamente</small><br>
      <input type="text" placeholder="nome" v-model="nomeField"><br>
      <input type="email" placeholder="email" v-model="emailField"><br>
      <input type="number" placeholder="idade" v-model="idadeField"><br>
      <button @click="cadastrarUsuario">Cadastrar</button>
      <hr>

   <div v-for="(cliente, index) in orderClientes" :key="cliente.id">
      <h4>{{index}}</h4>
      <Cliente :cliente="cliente" @meDelete="deletarUsuario($event)"/>
      
   </div>
   
  
  </div>
</template>

<script>

import _ from 'lodash';
import Cliente from './components/Cliente';
//import Produto from './components/Produto';
export default {
  name: 'App',
  data(){
    return{
    deuErro: false,
    nomeField: "",
    emailField: "",
    idadeField: 0,

    clientes: [
      {
        id:1,
        nome: "Fernando Dias",
        email: "fernando.dias@flex.com",
        idade: "34"
      },

      {
        id:2,
        nome: "Juliana Bela",
        email: "ju@jubelasdoces.com.br",
        idade: "35"
      },
      {
        id:3,
        nome: "Neco Belico",
        email: "neco@jubelasdoces.com.br",
        idade: "4"
      },
      {
        id:4,
        nome: "Preta Tinha",
        email: "preta@jubelasdoces.com.br",
        idade: "4"
      },
    ]


    }
  },
  components: {
   Cliente,
   //Produto
  },
  methods:{
    cadastrarUsuario: function(){
      if(this.nomeField=="" || this.nomeField == " " || this.nomeField.lenght < 3){
        
        this.deuErro = true;
      }else{
        this.deuErro = false;
        this.clientes.push({nome: this.nomeField, email: this.emailField, idade: this.idadeField, id: Date.now()});
        this.nomeField = "",
        this.emailField = "",
        this.idadeField = 0;
      }
      

    },
    deletarUsuario: function($event){
      console.log("recebendo evento");
      console.log($event.idDoCliente);
      var id = $event.idDoCliente;

      //uma maneira de remover o elemento do array
      var novoArray = this.clientes.filter(cliente => cliente.id != id);
      this.clientes = novoArray;
    }

  },
  computed: {
    orderClientes: function(){
      return _.orderBy(this.clientes, ['id'],['desc']);
    }

  }
}
</script>

<style>
#nomeErro{
  color: red;
}
</style>
