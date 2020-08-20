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
            <form @submit.prevent="agregarCita">
                <div class="row">
                    <div class="input-field col s12">
                        <i class="material-icons prefix">healing</i>
                        <input type="text" required="required" v-model="agregarMotivo" id="agregarMotivo">
                        <label>Motivo</label>
                    </div>
                    <div class="input-field col s6">
                        <i class="material-icons prefix">date_range</i>
                        <input type="text" required="required" class="datepicker"  id="agregarFecha" v-model="agregarFecha">
                        <label>Fecha</label>
                    </div>
                    <div class="input-field col s6">
                        <i class="material-icons prefix">access_time</i>
                        <input type="text" required="required" class="timepicker" id="agregarHora" v-model="agregarHora" duration=10>
                        <label>Hora</label>
                    </div>
                    <div class="col s12">
                        <input class="btn waves-effect waves-light blue-grey right btn-large" type="submit" name="action">Reservar
                            <i class="material-icons right white-text">check</i>
            
                        <button class="btn waves-effect waves-light grey right btn-large" type="button" name="action" @click.prevent="cancelarCita">Cancelar
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
            //datos cita
            agregarFecha: '',
            agregarHora: '',
            agregarMotivo: ''
        }
    },
    methods:{        
        agregarCita() {            
            db.collection('citasDoctor').add({
                fecha: document.querySelector('.datepicker').value,
                hora: document.querySelector('.timepicker').value,
                motivo: this.agregarMotivo,
                nombre: this.$store.state.usuario.nombre
            })
            // Redireccionar
            .then(() => {
                alert('agregaste una cita')
                // Limpiar fomulario
                this.agregarFecha = '';
                this.agregarHora = '';
                this.agregarMotivo = '';
                this.$router.push('/')
            })
        },
        cancelarCita() {   
            this.$router.push('/')
        }
    },
    mounted: function()  {
        const fecha = document.querySelectorAll('.datepicker');
        M.Datepicker.init(fecha, {
            format: 'dddd dd.mm.yy',
            i18n: {
                cancel: 'Cancelar',
                clear: 'Limpiar',
                done: 'Ok',
                months: [ 'Enero', 'Febrero', 'Marzo', 'Abril', 'Mayo', 'Junio', 'Julio', 'Agosto', 'Septiembre', 'Octubre', 'Noviembre', 'Diciembre' ],
                monthsShort: [ 'Ene', 'Feb', 'Mar', 'Abr', 'May', 'Jun', 'Jul', 'Ago', 'Sep', 'Oct', 'Nov', 'Dic' ],
                weekdays: [ 'Domingo', 'Lunes', 'Martes', 'Miércoles', 'Jueves', 'Viernes', 'Sábado' ],
                weekdaysShort: [ 'Dom', 'Lun', 'Mar', 'Mie', 'Jue', 'Vie', 'Sab' ],
                weekdaysAbbrev: ['S','L','M','M','J','V','S']	
            }
        });
        
        const hora = document.querySelectorAll('.timepicker');
        M.Timepicker.init(hora, {
            i18n: {
                cancel: 'Cancelar',
                clear: 'Limpiar',
                done: 'Ok'
            },
            showClearBtn: true,
        });       
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