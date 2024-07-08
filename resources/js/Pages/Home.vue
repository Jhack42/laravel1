<template>
    <div>
        <h1>Hola, soy una página Inertia.js con Vue.js!</h1>
        <button @click="getData">Obtener Datos</button>
        <p>{{ message }}</p>
    </div>
</template>

<script>
export default {
    data() {
        return {
            message: ''
        }
    },
    methods: {
        getData() {
            axios.get('/api/data')
                .then(response => {
                    this.message = response.data.message;
                })
                .catch(error => {
                    console.error(error);
                });
        }
    }
}
</script>
