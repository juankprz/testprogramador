<template>
    <div class="container">
        <table class="table">
                <thead>
                    <tr>
                    <th scope="col">ID</th>
                    <th scope="col">Nombre</th>
                    <th scope="col">Correo</th>
                    <th scope="col">Telefono</th>
                     <th scope="col">Estado</th>
                    </tr>
                </thead>
                <tbody>




                            <tr v-for="usuario in usuarios.data" :key="usuario.id">
                            <td>{{usuario.id}}</td>
                            <td>{{usuario.name}}</td>
                            <td>{{usuario.email}}</td>
                            <td>{{usuario.telephone}}</td>
                            <td>{{usuario.status}}</td>
                            </tr>



                </tbody>
                </table>
                <button v-if=" current_page !=1" @click.prevent="prevpage()"> Anterior </button> <br> <button  @click.prevent="nextpage()" > Siguiente </button>  {{"pagina #"+ usuarios["current_page"]}}

    </div>
</template>

<script>

    export default {
        data () {
            return {
                usuarios: [],
               current_page:1,

            }
        },
    computed:{

    },
       mounted(){
         this.obtenerusuarios();
        console.log(this.usuarios['data'].map((usuario) => usuario.status.includes('activo')));
     },
        methods: {
            obtenerusuarios(){
                  axios.get('/api/').then(response => (this.usuarios = response.data))
            },
            nextpage(){

                   axios.get('/api?page='+this.current_page++).then(response => (this.usuarios = response.data))

            },
         prevpage(){

                if(this.current_page<=1){
                      axios.get('/api?page='+1).then(response => (this.usuarios = response.data))

                }else{
                      axios.get('/api?page='+this.current_page--).then(response => (this.usuarios = response.data))

                }

            }



        },

    }

</script>
