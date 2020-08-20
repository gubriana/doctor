<template>
    <div class="row">
        <div class="card-panel m12">
            <div class="row">
                <div class="col m12">
                    <h1 class="header light blue-grey-text text-lighten-2">Reserva tu cita</h1>
                    <p><span v-if="usuario">{{ usuario.nombre }}</span>, debes elegir fecha y hora para tu cita</p>
                </div>
            </div>
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
                    <div class="input-field col s12">
                        <i class="material-icons prefix">healing</i>
                        <input type="text" required="required" v-model="agregarMotivo">
                        <label>Motivo</label>
                    </div>
                    <div class="col s12">
                        <button class="btn waves-effect waves-light blue-grey right btn-large" type="submit" name="action" @click="agregarCita">Reservar
                            <i class="material-icons right white-text">check</i>
                        </button>
                        <button class="btn waves-effect waves-light grey right btn-large" type="submit" name="action" @click="cancelarCita">Cancelar
                            <i class="material-icons right white-text">close</i>
                        </button>
                    </div>
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
    computed: {
        usuario() {
            return this.$store.state.usuario;
        }
    },
    data() {
        return {
            //datos de nuestra cita
            agregarFecha: '',
            agregarHora: '',
            agregarMotivo: ''
        }
    },
    methods:{
        agregarCita() {
            db.collection('citasDoctor').add({
                fecha: this.agregarFecha,
                hora: this.agregarHora,
                motivo: this.agregarMotivo,
                nombre: this.$store.state.usuario.nombre
            })
            // Redireccionar
            .then(() => {
                this.$router.push('/')
            })
            // Limpiar fomulario
            this.agregarFecha = '';
            this.agregarHora = '';
            this.agregarMotivo = ''; 
        },
        cancelarCita() {   
            this.$router.push('/')
        }

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
button {
    margin: 4rem 0 4rem 4rem;
}
</style>   