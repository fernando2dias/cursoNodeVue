<template>
<div :class="{'cliente' : !isPremium, 'cliente-premium': isPremium}">
    
    <h2>Nome: {{cliente.nome}}</h2>
    <hr>
    <p>Email: {{cliente.email | processarEmail}}</p>
    <p>Idade: {{cliente.idade}}</p>
    <button @click="mudarCor">Mudar Cor!</button>
    <button @click="emitirEventoDelete">Deletar</button>
    <h4>Id Especial: {{idEspecial}}</h4> 

</div>



</template>

<script>
export default {
    data(){
        return{
            isPremium: false
        }
    },
    props:{
        cliente: Object
    },
    methods:{
        mudarCor: function($event){
            console.log($event);
            
            this.isPremium = !this.isPremium;
        },
        emitirEventoDelete: function(){
        console.log("emitindo do filho");
        this.$emit("meDelete", {idDoCliente: this.cliente.id ,curso: "Formação Node.js", emPromocao: true, component: this});
        },
        testar: function(){
            console.log("testando pra  valer");
            alert("Isso é um alert!");


        }

    },
    filters: {
        processarEmail: function(value){
            return value.toUpperCase();

        }
    },
    computed: {
        idEspecial: function(){
            return (this.cliente.email+this.cliente.nome+this.cliente.id).toUpperCase();
        }
    }

}
</script>

<style scoped>
.cliente{
    max-width: 600px;
    height: 180px;
    background: #eee;
    padding: 1%;
    margin-top: 2%;
}

.cliente-premium{
    background: #333;
    color: gold;
     padding: 1%;
    margin-top: 2%;
    max-width: 600px;
    height: 180px;
}
</style>