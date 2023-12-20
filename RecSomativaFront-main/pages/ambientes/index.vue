<script setup>


    // função useFetch vai chamar o backend como se fosse no Insomnia
    const { data: allambientes } = await useFetch('http://localhost:8000/ambientes?all',{
      key: 'ambientesRequest' 
    });

    //criando as variáveis que vão armazenar os dados do formulario html
    let name;  

    const saveAmbiente = async() => {
        //imprimindo no console do navegador APENAS PARA TESTE
        console.log("nome", name);

        await useFetch('http://localhost:8000/ambientes/',{
            method: 'POST',
        body:
        [{

		    nome: name  
              
        }], onResponse(){
                alert("ambiente saved");
                refreshNuxtData('ambienteRequest')
            }
       
        
         });
     }


</script>


<template>
    <div>
        <h1>Bem vindo aos nossos cargos</h1>
  


        <section v-for="ambientes in allambientes.data" :key="ambientes.id">
            
            <h3>Nome: {{ ambientes.nome }}</h3>
            <br>
            <hr>
            <br>
            
            <!-- <img :src="'http://localhost:8000' + tarefa.foto" alt="foto tarefa"> -->
            <!-- <NuxtLink :to="'/trips/' + image.tripFk"></NuxtLink> -->

            <!-- <NuxtLink :to="`/tarefas/${tarefa.id}`">
                <img :src="'http://localhost:8000' + tarefa.foto" alt="foto tarefa">
            </NuxtLink> -->
        </section>
        <br>
        <hr>
        <label for="add">Adicionar um novo ambiente: </label>
        <br>

        <section>
        <br>
            <label for="">nome do ambiente: </label> <input type="text" v-model="name"> <br><br>
            <button @click="saveAmbiente">Salvar ambiente</button>
         </section>
        <br><hr>
    </div>
</template>