<!-- Card.vue -->
<template>
    <div v-for="post in datos" class="max-w-sm rounded overflow-hidden shadow-lg">
        <img class="w-full" src="https://placekitten.com/300/200" alt="Gatito">
        <div class="px-6 py-4">
            <div class="font-bold text-xl mb-2">{{ post.title }}</div>
            <p class="text-gray-700 text-base">
                {{ post.body }}
            </p>
        </div>
        <div class="px-6 pt-4 pb-2">
            <span
                class="inline-block bg-gray-200 rounded-full px-3 py-1 text-sm font-semibold text-gray-700 mr-2">#TailwindCSS</span>
            <span
                class="inline-block bg-gray-200 rounded-full px-3 py-1 text-sm font-semibold text-gray-700 mr-2">#VueJS</span>
            <span
                class="inline-block bg-gray-200 rounded-full px-3 py-1 text-sm font-semibold text-gray-700">#CardExample</span>
        </div>
    </div>
</template>
  
<script>
export default {
    data() {
        return {
            datos: [],
        };
    },

    props: {
        title: String,
        content: String,
        id: String
    },
    methods: {
        datosTabla(userId) {
            const apiUrl = `https://jsonplaceholder.typicode.com/posts?userId=${userId}`;

            fetch(apiUrl)
                .then((response) => response.json())
                .then((data) => {
                    this.datos = data; // Almacenamos los datos de la API en la variable 'datos'
                    console.log(this.datos, "aca");
                })
                .catch((error) => {
                    console.error("Error fetching data:", error);
                });
        },
    },
    mounted() {
        // En el hook mounted, puedes realizar la petición a la API y obtener los datos
        this.datosTabla(this.id)
    },
};
</script>
  
<style scoped>
/* Agrega estilos específicos del componente aquí si es necesario */
</style>
  