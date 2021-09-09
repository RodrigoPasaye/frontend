<template>
    
    <div class="container">

        <div class="card">

            <div class="card-header">
              <h4>Editar Cliente</h4>
            </div>

            <div class="card-body">

                <form v-on:submit.prevent="actualizarRegistro">

                    <div class="form-group">
                      <label for="nombre">Nombre:</label>
                      <input type="text"
                        class="form-control" name="nombre" v-model="cliente.nombre" id="nombre" aria-describedby="helpId" required placeholder="">
                      <small id="helpId" class="form-text text-muted">Escribe el nombre del cliente</small>
                    </div>

                    <div class="form-group">
                      <label for="apellidoPaterno">Apellido Paterno:</label>
                      <input type="text"
                        class="form-control" name="apellidoPaterno" v-model="cliente.apellidoPaterno" id="apellidoPaterno" aria-describedby="helpId" required placeholder="">
                      <small id="helpId" class="form-text text-muted">Escribe el apellido paterno del cliente</small>
                    </div>

                    <div class="form-group">
                      <label for="apellidoMaterno">Apellido Materno:</label>
                      <input type="text"
                        class="form-control" name="apellidoMaterno" v-model="cliente.apellidoMaterno" id="apellidoMaterno" aria-describedby="helpId" required placeholder="">
                      <small id="helpId" class="form-text text-muted">Escribe el apellido materno del cliente</small>
                    </div>

                    <div class="form-group">
                      <label for="rfc">RFC:</label>
                      <input type="text"
                        class="form-control" name="rfc" v-model="cliente.rfc" id="rfc" aria-describedby="helpId" required placeholder="">
                      <small id="helpId" class="form-text text-muted">Escribe el RFC del cliente</small>
                    </div>

                    <div class="form-group">
                      <label for="curp">CURP:</label>
                      <input type="text"
                        class="form-control" name="curp" v-model="cliente.curp" id="curp" aria-describedby="helpId" required placeholder="">
                      <small id="helpId" class="form-text text-muted">Escribe la CURP del cliente</small>
                    </div>

                    <br>

                    <div class="btn-group" role="group" aria-label="">
                        <router-link :to="{name:'Listar'}" class="btn btn-danger">Cancelar</router-link>
                        |                    
                        <button type="submit" class="btn btn-primary">Modificar</button>
                    </div>

                </form>

            </div>
            <div class="card-footer text-muted">

            </div>
        </div>

    </div><br>

</template>

<script>
  export default {
    data(){
      return{

        cliente:{}
      }
    },

    created:function(){

      this.obtenerInformacionID();

    },

    methods:{

      obtenerInformacionID(){

        fetch('http://localhost/API_REST_PHP/clientes.php?consultar='+this.$route.params.id)
        .then(respuesta=>respuesta.json())        
        .then((datosRespuesta)=>{
                  
          console.log(datosRespuesta)
          this.cliente = datosRespuesta[0];
          
        })
        .catch(console.log)

      },

      actualizarRegistro(){
        var datosEnviar = {idCliente:this.$route.params.id, nombre:this.cliente.nombre, apellidoPaterno:this.cliente.apellidoPaterno, apellidoMaterno:this.cliente.apellidoMaterno, rfc:this.cliente.rfc, curp:this.cliente.curp}

        fetch('http://localhost/API_REST_PHP/clientes.php?actualizar='+this.$route.params.id,{
                
          method:"POST",
          body:JSON.stringify(datosEnviar)

        })
        
        .then(respuesta=>respuesta.json())
        .then((datosRespuesta=>{

          console.log(datosRespuesta);
          window.location.href='../listar'

        }))

      }

    }
  }
</script>