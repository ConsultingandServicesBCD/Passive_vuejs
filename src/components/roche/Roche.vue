<template>
  <div class="ContenedorPrincipal">
        <div class="rutas">
  <InputData @accion='GetData'/>
  </div>
   <div class="respuesta">
      <MostrarRMS :rms='array_rms'/>
      
     </div> 
       <router-link to="/" class="home">home </router-link>
  </div>
</template>

<script>
import VueRouter from 'vue-router'
import InputData from '../componentes_Funcionales/InputData'
import KitPassive from './../../modulos/KitPassive'
import MostrarRMS from '../componentes_Funcionales/MostrarRMS'
export default {
    data() {
      return {
        array_rms: []
      }
    },
components: {
 VueRouter,
 InputData,
 MostrarRMS
},
methods: {
    GetData(data) {
       var texto_valor=data;
    //reseteamos el array para no concatenar información de los futuras ejecuciones
    this.array_rms=[]
var crearRM= (textrm,exprm)=>{
var buscarmatch=KitPassive.buscar_Match(exprm,texto_valor);
var crearRM=textrm+buscarmatch
console.log(buscarmatch)
this.array_rms.push(crearRM);
}

      //RM *ACECRM/R23-inicio      
      crearRM('RM *ACECRM/R23-',/(?<=WBS\sCECO\s)\d{0,}/)
      //RM *ACECRM/R23-fin

      //RM *ACECRM/R24-inicio
      crearRM('RM *ACECRM/R24-',/(?<=CUENTA\sDE\sGASTOS\s)\d{0,}/)
      //RM *ACECRM/R24-fin

      //RM *ACECRM/R25-inicio
      crearRM('RM *ACECRM/R25-',/(?<=Nº\nMOTIVO\s{0,}NO\s{0,}ANTELACION\s{0,})\w.*/)
      //RM *ACECRM/R25-fin

      //RM *ACECRM/R26-inicio
      crearRM('RM *ACECRM/R26-',/(?<=EMPLEADO\sSOLICITANTE\sY\s)\d{0,}/)
      //RM *ACECRM/R26-fin

      //RM *ACECRM/R27-inicio
      crearRM('RM *ACECRM/R27-',/^\w\d{0,}/)
      //RM *ACECRM/R27-fin 

      //RM *ACC inicio
        crearRM('RM *ACC',/^\w\d{0,}/)
      //RM *ACC fin

      //RM *ACECRM/REATRP- inicioL
        crearRM('RM *ACECRM/REATRP-',/(?<=MOTIVO\s{0,}DEL\s{0,}VIAJE\s{0,})\w/)
      //RM *ACECRM/REATRP-fin
      
      //RM *ACECRM/TQ3CD3-inico
        crearRM('RM *ACECRM/TQ3CD3-',/(?<=\n)\d{0,}(?=\s{0,}\w\s{0,}\C\d{0,}\w{2})/)
      //RM *ACECRM/TQ3CD3-fin
      console.log(this.array_rms)
    }
},
}
</script>

<style>

.respuesta{
grid-column: 2;
    grid-row: 1/11;
    display: flex;
    justify-content: center;
        padding-top: 111px;
}

</style>