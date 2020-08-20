<template>
    <div class="row">
        <div class="card-panel m12">
            <div class="row">
                <div class="col m11">
                    <h1 class="header light blue-grey-text text-lighten-2">Agenda tu cita</h1>
                    <p><span v-if="usuario">{{ usuario.nombre }}</span>, podrás agendar tu próxima visita al doctor aquí</p>
                </div>
                <div class="col m1">
                    <router-link v-bind:to="{ path: '/reservar' }" class="btn-floating btn-large waves-effect waves-light blue-grey"><i class="material-icons">add</i></router-link>
                    <!-- <a class="btn-floating btn-large waves-effect waves-light blue-grey"><i class="material-icons">add</i></a> -->
                </div>
            </div>
            <br>
            <nav>
                <div class="nav-wrapper blue-grey lighten-3">
                <form>
                    <div class="input-field">
                    <input id="search" type="search" required>
                    <label class="label-icon" for="search"><i class="material-icons">search</i></label>
                    <i class="material-icons">close</i>
                    </div>
                </form>
                </div>
            </nav>
        </div>

        <div class="col m12">
            <table class="striped responsive-table highlight" >
                <thead>
                    <tr>
                        <th>Fecha</th>
                        <th>Hora</th>
                        <th>Nombre</th>
                        <th>Motivo</th>
                        <th>Eliminar</th>
                    </tr>
                </thead>

                <tbody>
                    <tr v-for="cita in citasDoctor" :key="cita.id">
                        <td>{{cita.fecha}}</td>
                        <td>{{cita.hora}}</td>
                        <td>{{cita.nombre}}</td>
                        <td>{{cita.motivo}}</td>
                        <td><button @click.prevent="borrarCita(cita.id)"> <i class="material-icons" >delete</i></button></td>
                    </tr>
                </tbody>
            </table>
        </div>
    </div>
</template>
<script>
import { db } from '@/firebase.js'

export default {
    name: 'CitasDoctor',
    data() {
        return {
            citasDoctor: []
        }
    },
    computed: {
        usuario() {
            return this.$store.state.usuario;
        }
    },
    methods: {
        borrarCita(id) {
            const respuesta = confirm('¿Quieres borrar esta cita?');
            if (respuesta == false) { return; }
            db.collection("citasDoctor").doc(id).delete();
        }
    },
    firestore() {           // adding this key/function
        return {
            citasDoctor: db.collection('citasDoctor')
        }
    }
    
}
</script>
<style scoped>
.btn-floating {
    margin-top: 4rem;
}
.card-panel {
    margin-top:4rem;
}
</style>   