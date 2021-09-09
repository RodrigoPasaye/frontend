<template>
    <div class="container">

        <div class="text-center">
            <h1>Sistema de Administración de Usuarios</h1>
        </div>
        <br><br>

        <router-link to="/crear" class="btn btn-primary">Registrar nuevo Cliente</router-link>
        <br><br><br>

        <div class="card">

            <div class="card-header">
                <h4>Clientes activos</h4>
            </div>

            <div class="card-body">

                <table class="table table-hover">
                    <thead class="thead-light">
                        <tr>
                            <th>ID</th>
                            <th>Nombre</th>
                            <th>Apellido Paterno</th>
                            <th>Apellido Materno</th>
                            <th>RFC</th>
                            <th>CURP</th>
                            <th>Acciones</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr v-for="cliente in clientes" :key="cliente.idCliente">
                            <td> {{cliente.idCliente}} </td>
                            <td> {{cliente.nombre}} </td>
                            <td> {{cliente.apellidoPaterno}} </td>
                            <td> {{cliente.apellidoMaterno}} </td>
                            <td> {{cliente.rfc}} </td>
                            <td> {{cliente.curp}} </td>
                            <td>

                                <router-link :to="{name:'Ver', params:{id:cliente.idCliente}}" class="btn btn-warning">Ver</router-link>
                                |
                                <router-link :to="{name:'Editar', params:{id:cliente.idCliente}}" class="btn btn-warning">Editar</router-link>
                                |
                                <button type="button" v-on:click="borrarCliente(cliente.idCliente)" class="btn btn-danger">Eliminar</button>


                            </td>
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

        this.consultarClientes();

    },

    methods:{
        
        consultarClientes(){

            fetch('http://localhost/API_REST_PHP/clientes.php')
            .then(respuesta=>respuesta.json())
            .then((datosRespuesta)=>{
                
                console.log(datosRespuesta)

                this.clientes=[]
                if(typeof datosRespuesta[0].success==='undefined'){
                    this.clientes = datosRespuesta;
                }
            })
            .catch(console.log)
        },

        borrarCliente(id){

            console.log(id);

            fetch('http://localhost/API_REST_PHP/clientes.php?borrar='+id)
            .then(respuesta=>respuesta.json())
            .then((datosRespuesta)=>{
                
                console.log(datosRespuesta)
                window.location.href='listar'

            })
            .catch(console.log)


        }
    }
    
}
</script>