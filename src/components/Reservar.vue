<template>
    <div class="row">
        <div class="card-panel m12">
            <div class="row">
                <div class="col m12">
                    <h1 class="header light blue-grey-text text-lighten-2">Reserva tu cita</h1>
                    <p><span v-if="usuario">{{ usuario.nombre }}</span>, debes elegir fecha y hora para tu cita</p>
                </div>
            </div>
            <hr class="red">
            <br>
            <form @submit="agregarCita">
                <div class="row">
                    <div class="input-field col s6">
                        <i class="material-icons prefix">date_range</i>
                        <input type="text" required="required" class="datepicker" v-model="agregarFecha">
                        <label>Fecha</label>
                    </div>
                    <div class="input-field col s6">
                        <i class="material-icons prefix">access_time</i>
                        <input type="text" required="required" class="timepicker" v-model="agregarHora">
                        <label>Hora</label>
                    </div>
                    <div class="input-field col s8">
                        <i class="material-icons prefix">healing</i>
                        <input type="text" required="required" v-model="Motivo">
                        <label>Motivo</label>
                    </div>
                    <button class="btn waves-effect waves-light blue-grey right btn-large" type="submit" name="action">Reservar
                        <i class="material-icons right white-text">check</i>
                    </button>
                </div>
            </form>
        </div>
    </div>
</template>
<script>
import M from 'materialize-css' 
import { db } from '@/firebase.js'

export default {
    name: 'reservar',
    data() {
        return {
            //datos de nuestra cita
            agregarFecha: '',
            agregarHora: '',
            agregarMotivo: '',
        }
    },
    computed: {
        usuario() {
            return this.$store.state.usuario;
        }
    },
    methods:{

    },
    mounted: function()  {
        M.AutoInit();
        const date = document.querySelectorAll('.datepicker');
        M.Datepicker.init(date, {});
        const time = document.querySelectorAll('.timepicker');
        M.Timepicker.init(time, {});
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