<template>
  <q-page>
    <div class="row">
      <div class="col-12">
        <q-form @submit.prevent="crear">
          <div class="row q-pa-xs">
            <div class="col-1">
              <q-input type="text" outlined dense label="Paterno" required v-model="estudiante.Paterno"/>
            </div>
            <div class="col-1">
              <q-input type="text" outlined dense label="Materno" required v-model="estudiante.Materno"/>
            </div>
            <div class="col-2">
              <q-input type="text" outlined dense label="Nombres" required v-model="estudiante.Nombres"/>
            </div>
            <div class="col-1">
              <q-input type="number" outlined dense label="CI" required v-model="estudiante.CI"/>
            </div>
            <div class="col-2">
              <q-input type="date" outlined dense label="Fec. Nac." required v-model="estudiante.Fechanacimiento"/>
            </div>
            <div class="col-1">
            <q-input type="text" outlined dense label="Sexo" required v-model="estudiante.Sexo"/>
            </div>
            <div class="col-2">
              <q-input type="number" outlined dense label="Celular" required v-model="estudiante.Celular"/>
            </div>
            <div class="col-2 flex flex-center">
              <q-btn type="submit" outlined dense icon="send" :color="boolcrear?'positive':'yellow'" :label="boolcrear?'Insertar':'Modificar'"/>
            </div>
          </div>
        </q-form>
      </div>
      <div class="col-12">
        <q-table title="ESTUDIANTES" :columns="columns" :rows="estudiantes" dense>
          <template v-slot:body="props">
            <q-tr :props="props">
              <q-td key="id" :props="props">
                <q-badge>{{props.row.id}}</q-badge>
              </q-td>
              <q-td key="Paterno" :props="props">
                <q-badge color="teal" >{{props.row.Paterno}}</q-badge>
              </q-td>
              <q-td key="Materno" :props="props">
                <q-badge color="negative">{{props.row.Materno}}</q-badge>
              </q-td>
              <q-td key="Nombres" :props="props">
                <q-badge color="purple">{{props.row.Nombres}}</q-badge>
              </q-td>
              <q-td key="CI" :props="props">
                <q-badge color="blue">{{props.row.CI}}</q-badge>
              </q-td>
              <q-td key="Fechanacimiento" :props="props">
                <q-badge color="pink">{{props.row.Fechanacimiento}}</q-badge>
              </q-td>
              <q-td key="Sexo" :props="props">
                <q-badge color="negative">{{props.row.Sexo}}</q-badge>
              </q-td>
              <q-td key="Celular" :props="props">
                <q-badge color="orange">{{props.row.Celular}}</q-badge>
              </q-td>
              <q-td key="opciones" :props="props">
                <q-btn @click="eliminar(props.row)" size="xs" icon="delete" color="negative"  label="Eliminar"/>
                <q-btn @click="modificar(props.row)" size="xs" icon="edit" color="primary"  label="Modifica"/>
              </q-td>
            </q-tr>
          </template>
        </q-table>
      </div>
    </div>
  </q-page>
</template>
<script>
import {date} from 'quasar'
export default {
  data(){
    return {
      estudiantes:[],
      estudiante:{Paterno:'',Materno:'',Nombres:'',CI:'',Fechanacimiento:date.formatDate(Date.now(),'YYYY-MM-DD'),Sexo:'',Celular:''},
      boolcrear:true,
      columns:[
        {name:'id',label:'Id',field:'id'},
        {name:'Paterno',label:'APELLIDO PATERNO',field:'Paterno'},
        {name:'Materno',label:'APELLIDO MATERNO',field:'Materno'},
        {name:'Nombres',label:'NOMBRES',field:'Nombres'},
        {name:'CI',label:'CI',field:'CI'},
        {name:'Fechanacimiento',label:'F. NACIMIENTO',field:'Fechanacimiento'},
        {name:'Sexo',label:'SEXO',field:'Sexo'},
        {name:'Celular',label:'CELULAR',field:'Celular'},
        {name:'opciones',label:'OPCIONES',field:'opciones'},     
      ]
    }
  },
  created() {
    this.misdatos()
  },
  methods:{
    crear(){
      this.$q.loading.show()
      if (this.boolcrear)
        this.$api.post('/estudiante',this.estudiante).then(res=>{
          this.estudiante={Fechanacimiento:date.formatDate(Date.now(),'YYYY-MM-DD')}
          this.misdatos()
          this.$q.loading.hide()
        })
      else
        this.$api.put('/estudiante/'+this.estudiante.id,this.estudiante).then(res=>{
          this.estudiante={Fechanacimiento:date.formatDate(Date.now(),'YYYY-MM-DD')}
          this.misdatos()
          this.boolcrear=true
          this.$q.loading.hide()
        })
    },
    misdatos(){
      this.$api.get('/estudiante').then(res=>{
        this.estudiantes=res.data
        console.log(this.estudiantes)
      })
    },
    eliminar(estudiante){
      this.$q.loading.show()
      if (confirm("Seguro de eliminar?"))
        this.$api.delete('/estudiante/'+estudiante.id).then(res=>{
          this.misdatos()
          this.$q.loading.hide()
        })
        this.$q.loading.hide()
    },
    modificar(estudiante){
      this.estudiante=estudiante
      this.boolcrear=false
    }
  }
}
</script>

<style scoped>

</style>
