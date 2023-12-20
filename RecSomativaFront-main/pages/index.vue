<script setup>
    definePageMeta({
        layout: "loginlay"
    });
    // função useFetch vai chamar o backend como se fosse no Insomnia
    const { data: allLogin } = await useFetch('http://localhost:8000/usuarios',{
      key: 'usuarioRequest' 
    });

</script>


<template>
    <div>
        <h1>
            bem vindo ao login
        </h1>
        <h3 >Insira suas informações abaixo!!</h3>
        <label for="">Email: </label>
        <select v-model="emails">
        <option value=""></option>

        <option v-for="usuarios in allLogin.data" :key="usuarios.id">
            
           {{ usuarios.email }}
          


        </option>
       
        </select>
        <p>
        <label for="senha">Senha:</label>
        <br>
        <input
           id="senha"
           v-model="senha"
           type="text"
           senha="senha">
        </p>
        <br>
        <br>
        <NuxtLink to="/homePage"> <!-- Basta mudar aqui quando funcionar o homePage/ID-->
        <button v-if="emails  !== ''" @click="realizarAcao ">Login</button>
        </NuxtLink>
        <br>


    </div>
</template>

<style>
  div{
    display: flex;
    flex-direction: column;  
    justify-content: center;
    align-content: center;
  }

  select{
    width: 300px;
  }

</style>
<script>
export default {
  data() {
    return {
      emails: '' // Inicializa a variável para armazenar a opção selecionada
    };
  }
};
</script>