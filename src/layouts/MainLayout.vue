<template>
  <q-layout lu>
    <q-header >
      <q-toolbar >
        <q-btn 
          flat
          dense
          round
          
          icon="menu"
          aria-label="Menu"
          @click="toggleLeftDrawer"
        />

        <q-toolbar-title >
          FRONTEND COLEGIO
        </q-toolbar-title>

        <!-- <div>Quasar v{{ $q.version }}</div> -->
      </q-toolbar>
    </q-header>

    <q-drawer
      v-model="leftDrawerOpen"
      show-if-above
      bordered
    
    >
      <q-list>
        <q-item-label
          header
        >
         #MENU - COLEGIO
        </q-item-label>

        <q-item to="materia" clickable v-ripple>
          <q-item-section>MATERIAS</q-item-section>
          <q-item-section avatar>
            <q-icon  color="purple" name="calculate" />
          </q-item-section>
        </q-item>
        <q-item to="docente" clickable v-ripple>
          <q-item-section>DOCENTES</q-item-section>
          <q-item-section avatar>
            <q-icon   color="purple" name="people" />
          </q-item-section>
        </q-item>
        <q-item to="estudiante" clickable v-ripple>
          <q-item-section>ESTUDIANTES</q-item-section>
          <q-item-section avatar>
            <q-icon color="purple" name="people" />
          </q-item-section>
        </q-item>

      </q-list>
    </q-drawer>

    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script>

export default {
  name: 'MainLayout',
  data(){
    return{
      leftDrawerOpen:false
    }
  },
  methods:{
        toggleLeftDrawer () {
          this.leftDrawerOpen = !this.leftDrawerOpen
        }
  }

  // setup () {
  //   const leftDrawerOpen = ref(false)
  //
  //   return {
  //     leftDrawerOpen,
  //     toggleLeftDrawer () {
  //       leftDrawerOpen.value = !leftDrawerOpen.value
  //     }
  //   }
  // }
}
</script>
