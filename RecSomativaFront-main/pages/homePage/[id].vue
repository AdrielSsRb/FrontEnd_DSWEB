<script setup>
    const route = useRoute();

    const {data: ussFound} = await useFetch(`http://localhost:8000/tarefas?solicitante=${route.params.id}`,{
      key: 'tarefastussRequest' });

    const { data: userFound } = await useFetch(`http://localhost:8000/usuarios/${route.params.id}`,{
      key: 'usuarioRequest' 
    });


    const teste = await route.params.id
</script>


<template>
    <div>
        <section>
            <h1>
                oi {{ ussFound.data.nome }}
            </h1>
        </section>
        <br>
        <section>
            <h3>Status: {{ ussFound.data.idStatusFK.nome }}</h3>
            <h3>Ambiente: {{ ussFound.data.idAmbienteFK.nome }}</h3>
            <h3>Prazo: {{ ussFound.data.prazo }}</h3>
        </section>
    </div>
</template>
