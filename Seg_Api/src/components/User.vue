<template>
    <div class="container mx-auto w-full">
        <h1 class="text-2xl font-bold mb-4">Lista de usuarios</h1>
        <div class="overflow-x-auto w-full">
            <div v-if="mostrarContenido">
                <button @click="Ocultarcontenido()"
                    class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-1 px-2 rounded focus:outline-none focus:shadow-outline-blue active:bg-blue-800">
                    regresar
                </button>

            </div>

            <div v-if="!mostrarContenido">
                <table class=" w-full  border-collapse border border-gray-300">
                    <thead>
                        <tr class="bg-gray-200">
                            <th class="border border-gray-300 px-4 py-2">ID</th>
                            <th class="border border-gray-300 px-4 py-2">Nombre</th>
                            <th class="border border-gray-300 px-4 py-2">Nombre de usuario</th>
                            <th class="border border-gray-300 px-4 py-2">Correo electrónico</th>
                            <th class="border border-gray-300 px-4 py-2">Domicilio</th>
                            <th class="border border-gray-300 px-4 py-2">Teléfono</th>
                            <th class="border border-gray-300 px-4 py-2">Sitio web</th>
                            <th class="border border-gray-300 px-4 py-2">Empresa</th>
                            <th class="border border-gray-300 px-4 py-2">Ver</th>

                            <!-- Agrega más encabezados aquí según sea necesario -->
                        </tr>
                    </thead>
                    <tbody>
                        <tr v-for="user in users" :key="user.id">
                            <td class="border border-gray-300 px-4 py-2">{{ user.id }}</td>
                            <td class="border border-gray-300 px-4 py-2">{{ user.name }}</td>
                            <td class="border border-gray-300 px-4 py-2">{{ user.username }}</td>
                            <td class="border border-gray-300 px-4 py-2">{{ user.email }}</td>
                            <td class="border border-gray-300 px-4 py-2">{{ user.address.street }}</td>
                            <td class="border border-gray-300 px-4 py-2">{{ user.phone }}</td>
                            <td class="border border-gray-300 px-4 py-2">{{ user.website }}</td>
                            <!-- Agrega esto dentro de tu celda <td> -->
                            <td class="border border-gray-300 px-4 py-2">
                                {{ user.company.name }}
                            </td>
                            <td class="border border-gray-300 px-4 py-2">
                                <button @click="toggleMostrarContenido(user.id)"
                                    class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-1 px-2 rounded focus:outline-none focus:shadow-outline-blue active:bg-blue-800">
                                    Ver post
                                </button>
                            </td>
                            <!-- Agrega más celdas aquí según sea necesario -->
                        </tr>
                    </tbody>
                </table>

            </div>

            <div v-if="mostrarContenido">
                <TuComponenteTabla :id="idSelect" />
            </div>

        </div>
    </div>
</template>

<script>
import TuComponenteTabla from './PostsUser.vue';

export default {
    components: {
        TuComponenteTabla,
    },
    data() {
        return {
            mostrarContenido: false,
            users: [], // Aquí almacenaremos los datos de la API
            datos: [],
            idSelect: null,
        };
    },

    methods: {
        datosTabla() {
            fetch("https://jsonplaceholder.typicode.com/users")
                .then((response) => response.json())
                .then((data) => {
                    this.users = data; // Almacenamos los datos de la API en la variable users
                })
                .catch((error) => {
                    console.error("Error fetching data:", error);
                });
        },
        toggleMostrarContenido(id) {
            this.idSelect = id;
            // Cambiar el valor de mostrarContenido al contrario (true a false o false a true)
            this.mostrarContenido = !this.mostrarContenido;
        },
        Ocultarcontenido() {
            this.mostrarContenido = !this.mostrarContenido;
        }
    },

    mounted() {
        // En el hook mounted, puedes realizar la petición a la API y obtener los datos
        this.datosTabla()
    },
};
</script>

<style scoped>
/* Estilos específicos de Tailwind CSS para el componente */
/* Puedes agregar más estilos según sea necesario */
/* No olvides configurar Tailwind en tu proyecto para que estos estilos se apliquen correctamente */
.container {
    padding: 2rem;
}

.text-2xl {
    font-size: 1.5rem;
}

.font-bold {
    font-weight: bold;
}

.mb-4 {
    margin-bottom: 1rem;
}

.min-w-full {
    width: 100%;
}

.border-collapse {
    border-collapse: collapse;
}

.border {
    border: 1px solid #e2e8f0;
}

.bg-gray-200 {
    background-color: #edf2f7;
}

.px-4 {
    padding-left: 1rem;
    padding-right: 1rem;
}

.py-2 {
    padding-top: 0.5rem;
    padding-bottom: 0.5rem;
}
</style>
