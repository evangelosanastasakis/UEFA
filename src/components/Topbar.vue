<template>
  <div>
    <v-app-bar
      color="indigo darken-4"
      class="white--text text" >
     <v-toolbar-title>UEFA Champions League</v-toolbar-title>

     <div class="flex-grow-1" ></div>

     <v-btn text small to="/">Home</v-btn>
     <v-btn text small to="/teams">Teams</v-btn>
     <v-btn text small to="/about">About</v-btn>
     <v-btn text small to="/contact">Contact</v-btn>
    </v-app-bar>
  </div>
</template>

<script>
export default {
  name: 'Topbar'
}
</script>
<style> 
 
  
  

</style>