<script setup>
// função useFetch vai chamar o backend como se fosse no Insomnia
    const { data: allcargos } = await useFetch('http://localhost:8000/cargos?all',{
      key: 'cargosRequest' 
    });

    //criando as variáveis que vão armazenar os dados do formulario html
    let cargo;  

    const saveCargo = async() => {
        //imprimindo no console do navegador APENAS PARA TESTE
        console.log("cargo", cargo);

        await useFetch('http://localhost:8000/cargos/',{
            method: 'POST',
        body:
        [{

		    nome: cargo  
              
        }], onResponse(){
                alert("cargo saved");
                refreshNuxtData('cargosRequest')
            }
       
        
         });
     }
    
    
</script>


<template>
    <div>
        <h1>Bem vindo aos nossos cargos</h1>
        <section v-for="cargos in allcargos.data" :key="cargos.id">
            
            <h3>Nome: {{ cargos.nome }}</h3>
            <h3>nivelAcesso: {{ cargos.nivelAcesso }}</h3>
            <br>
            <hr>
 
        </section>
   

            <section>
            <label for="add">Adicionar um novo cargo: </label>
            <br>
            <br>
            <label for="">nome do Cargo: </label> <input type="text" v-model="cargo"> <br><br>
            <button @click="saveCargo">Salvar cargo</button>
            </section>
            <br><hr>

        <br><hr>
    </div>
</template>