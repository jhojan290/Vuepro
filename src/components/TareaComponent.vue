<template>
    <div>
        <h1 class="display-4 text-center">Listado de Tareas</h1>
        <hr>
        <div class="row">
            <div class="col-lg-8 offset-lg-2">
                <div class="card mt-4">
                    <div class="card-body">
                        <div class="input-group">
                            <input type="text" v-model="tarea"
                                class="form-control form-control lg" placeholder="Agregar-Tarea">
                            <div class="input-group-append">
                                <button v-on:click="AgregarTarea()"
                                class="btn btn-success btn-lg">Agregar</button>
                            </div>
                        </div>
                        <br>

                        <h5 v-if="ListTareas.length == 0">No hay tareas para realizar</h5>
                        <ul class="list-group">
                            <li v-for="(tarea, index) of ListTareas" :key="index"
                                class="list-group-item d-flex justify-content-between">
                                <span class="cursor" v-bind:class="{'text-success': tarea.estado}"
                                     v-on:click="editarTarea(tarea, index)">
                                    <i v-bind:class="[tarea.estado ? 'fa-solid fa-circle-check' : 'fa-regular fa-circle']"></i>
                
                                </span>
                                {{ tarea.nombre }}
                                <span class="text-danger cursor" v-on:click="eliminarTarea(index)">
                                    <i class="fa-solid fa-trash"></i>
                                </span>
                            </li>
                        </ul>
                    </div>
                </div> 
            </div>
        </div>
    </div>
</template>

<script>

    export default {
        name: 'TareaComponent',
        data(){
            return {
                tarea:'',
                ListTareas : []
            }
        },
        methods: {
            AgregarTarea(){
                const tarea = {
                    nombre: this.tarea,
                    estado: false
                }
                this.ListTareas.push(tarea);
                this.tarea = '';
            },
            eliminarTarea(index){
                this.ListTareas.splice(index, 1)
            },
            editarTarea(tarea, index){
                this.ListTareas[index].estado = !tarea.estado
            }
        }
    }

</script>

<style>
.cursor{
    cursor:pointer;   
}
</style>
