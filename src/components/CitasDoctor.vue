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
            <hr>
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
            <table class="striped responsive-table highlight">
                <thead>
                <tr>
                    <th>Fecha</th>
                    <th>Hora</th>
                    <th>nombre</th>
                    <th>Motivo</th>
                    <th>Eliminar</th>
                </tr>
                </thead>

                <tbody>
                <tr>
                    <td>12.02.20</td>
                    <td>15.30</td>
                    <td>Gabri</td>
                    <td>Dolor de panza</td>
                    <td><i class="material-icons">delete</i></td>
                </tr>
                <tr>
                    <td>18.12.20</td>
                    <td>15.30</td>
                    <td>Mr.A</td>
                    <td>Control</td>
                    <td><i class="material-icons">delete</i></td>
                </tr>
                <tr>
                    <td>15.02.20</td>
                    <td>11.30</td>
                    <td>Rodri</td>
                    <td>Malesta estomacal</td>
                    <td><i class="material-icons">delete</i></td>
                </tr>
                </tbody>
            </table>
        </div>
    </div>
</template>
<script>

export default {
    name: 'CitasDoctor',
    computed: {
        usuario() {
            return this.$store.state.usuario;
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