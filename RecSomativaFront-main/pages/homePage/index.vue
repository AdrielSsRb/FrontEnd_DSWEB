<script setup>

    // função useFetch vai chamar o backend como se fosse no Insomnia
    const { data: allLogin } = await useFetch('http://localhost:8000/usuarios?all',{
      key: 'usuarioRequest' 
    });

</script>

<template>
    <div>
        <section v-for="usuarios in allLogin.data" :key="usuarios.id">
            
            <h3>Ola {{ usuarios.nome }}</h3>
            <h3>seu ID{{ usuarios.idUserFK }}</h3>
            <br>
            <hr>

        </section>
    </div>
</template>