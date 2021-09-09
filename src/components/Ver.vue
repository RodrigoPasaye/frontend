<template>
    <div class="container">

        <div class="text-center">
            <h1>Sistema de Administración de Usuarios</h1>
        </div>
        <br><br>

        <router-link :to="{name:'Listar'}" class="btn btn-primary">Regresar</router-link> 
        <br><br><br>

        <div class="card">

            <div class="card-header">
                <h4>Ver Cuentas del Cliente</h4>
            </div>

            <div class="card-body">

                <table class="table table-hover">
                    <thead class="thead-light">
                        <tr>
                            <th>Cliente</th>
                            <th>Apellido Paterno</th>
                            <th>Nombre de la Cuenta</th>
                            <th>Saldo Actual</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr v-for="cliente in clientes" :key="cliente.idCliente">
                            <td> {{cliente.nombre}} </td>
                            <td> {{cliente.apellidoPaterno}} </td>
                            <td> {{cliente.nombreCuenta}} </td>
                            <td> {{cliente.saldoActual}} </td>
                        </tr>
                    </tbody>
                </table>

            </div>

            <div class="card-footer text-muted">

            </div>
        </div>


    </div><br><br>
</template>



<script>

export default {

    data(){

        return{
            clientes:[]
        }
    },

    created:function(){

        this.consultarCuenta();

    },

    methods:{
        
        consultarCuenta(){

            fetch('http://localhost/API_REST_PHP/clientes.php?consultarCuenta='+this.$route.params.id)
            .then(respuesta=>respuesta.json())
            .then((datosRespuesta)=>{
                
                console.log(datosRespuesta)

                this.clientes=[]
                if(typeof datosRespuesta[0].success==='undefined'){
                    this.clientes = datosRespuesta;
                }
            })
            .catch(console.log)
        }

    }
    
}
</script>