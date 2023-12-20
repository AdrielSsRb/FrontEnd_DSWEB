<script setup>
    // acessamos o mecanismo de rotas do NUXT
    const route = useRoute();
    const {data: tarefaFound} = await useFetch(`http://localhost:8000/tarefas/${route.params.id}`,{
      key: 'tarefaRequest' 
    });

    const {data: sttsFound} = await useFetch(`http://localhost:8000/tarefasStatus?tarefa=${route.params.id}`,{
      key: 'tarefasttsRequest' 
    });


    const {data: fotosFound} = await useFetch(`http://localhost:8000/fotos?tarefa=${route.params.id}`,{
      key: 'tarefasfotosRequest' 
    });



    const teste = await route.params.id
    
</script>

<template>
    <div>
      <h1>
        Seja bem vindo a tarefa {{ tarefaFound.data.nome}}</h1>
        <br>
        <section>
            <h3>Status: {{ tarefaFound.data.idStatusFK.nome }}</h3>
            <h3>Ambiente: {{ tarefaFound.data.idAmbienteFK.nome }}</h3>
            <h3>Prazo: {{ tarefaFound.data.prazo }}</h3>
        </section>
        <br>
        <section v-if="mostrar">
            <h3>Data de início: {{ tarefaFound.data.dataInicio }}</h3>
            <h3>Data término: {{ tarefaFound.data.dataFim }}</h3>
            <h3>Descrição: {{ tarefaFound.data.descricao }}</h3>
            <h3>Solicitante: {{ tarefaFound.data.idSolicitanteFK.nome }}</h3>
            <img :src="tarefaFound.data.idSolicitanteFK.image" alt="Imagem do solicitante">
            <p>Imagem do solicitante: {{ tarefaFound.data.idSolicitanteFK.nome }}</p>
            <h3>Histórico</h3>

            <section v-for="fotos in fotosFound.data" :key="fotos.id">
              <h3>Fotos da tarefa {{ fotos.nome }}:</h3>
              <br>
              <img :src="fotos.image" alt="fotos tarefas">
            </section>
            
            <h4 v-for="stts in sttsFound.data" :key="stts.id">  / Data: {{ stts.data.data }} / Descrição: {{ stts.data.descricao }}</h4>
           
        </section>
        <br>
        <label for="detalhes">Detalhes? </label>

   <button @click="exibirDescricao">Sim</button>

    <!-- Elemento para exibir a descrição -->
    <p v-if="mostrar">Detalhe exposto</p>

    <br>
    <br>  
        
    <br>
        <NuxtLink :to="`/tarefas`">
                <button>Voltar</button>
            </NuxtLink>
        <br>
        <hr>
    </div>

</template>


<script>
export default {
  data() {
    return {
      mostrar: false // Variável para controlar a exibição da descrição
    };
  },
  methods: {
    exibirDescricao() {
      // Função para mostrar a descrição
      this.mostrar = true;
    }
  }
};
</script>