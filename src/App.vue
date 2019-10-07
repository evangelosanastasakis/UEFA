<template>
 <v-app>
   <v-content>
     <topbar />
     <router-view />
   </v-content>
 </v-app>
</template>

<script>
import Topbar from './components/Topbar.vue'

export default {
 name: 'App',
 components: { Topbar }
}
</script>