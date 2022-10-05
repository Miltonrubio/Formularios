<script>
export default {
    data: () => ({
       proyecto:"",
       tipo:"",
       urgente:false,
      proyectos:[],
      numeroProyectos:0,
    }),
    methods: {

        cambiarUrgencia(proyecto, campo){
           // this.proyectos[id].urgente= !this.proyectos[id].urgente;
          console.log(proyecto, campo);
          proyecto[campo]=!proyecto[campo];

        },
        registrarProyecto(){
            const proyecto={
                proyecto: this.proyecto,
                tipo: this.tipo,
                urgente: this.urgente,
                completado:false,

            };
            this.proyectos.push(proyecto);
            this.proyecto="";
            this.tipo="";
            this.urgente=false;
            console.log(this.proyectos)    ;
        },
     
    }  , 
    computed:{
            numeroProyectos(){
                return this.proyectos.length;
            }
        }
};
</script>

<template>
   
    <div class="row">
        <div class="col-12 col-md-4">  <form @submit.prevent="registrarProyecto">
        <div class="mb-3">
            <label class="form-label"> Actividad </label>
            <input class="form-control" v-model.trim="proyecto" type="text" placeholder="Actividad" required />
      
            <!--
      <input class="form-control" v-model="nombre" type="text" placeholder="Nombre" required />
      
            <label class="form-label">Edad: </label>
            <input class="form-control" v-model="edad" type="number" min="15" max="80" placeholder="Edad" required />
      
            -->
       <select required v-model="tipo">
        <option disabled selected value=""  > Selecciona un tipo de actividad</option>
        <option value="1">Aplicaciones web con Vue.js</option>
        <option value="2">Backend Services con Node.js</option>
        <option value="3">App movil con react Native</option>
        
       </select>
        </div>
        <div class="mb-3">

            <label> urgente</label>
     <input type="checkbox" v-model="urgente" class="form-check-input" >

        </div>
        <button class="btn btn-success btn-block" type="submit">guardar</button>
    </form>  </div>


            <div class="col-12 col-md-8">



<h3> Total de proyectos: {{numeroProyectos}}</h3>   

   
                <div class="table-responsive">
        <table class="table table-dark ">
            <thead>
                <tr>
                    <th> #
            </th>
            <th>  proyecto
            </th>
            <th>  tipo
            </th>
            <th>  urgente
            </th>
            <th> Completado
            </th>
                </tr>
               
            </thead>
            <tbody>
                <tr v-for="(proyecto, index) in proyectos" :key="index" >
                    <td>{{index +1}}</td>
                    <td>{{proyecto.proyecto}}</td>
                    <td>{{proyecto.tipo}}</td>
                    <td @click="cambiarUrgencia(proyecto, 'urgente')" :class="proyecto.urgente ?  'bg-danger':'bg-success' " > {{proyecto.urgente ? "si" : "no" }}</td>
                    <td @click="cambiarUrgencia(proyecto, 'completado')" :class="proyecto.completado ?  'bg-success':'bg-danger' " > {{proyecto.completado ? "completado" : "incompleto" }}</td>
                 
                </tr>
                
              
            </tbody>
           
        </table>
    </div>
            </div>
     
    </div>
</template>