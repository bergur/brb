<template>
    <v-ons-page>
      <custom-toolbar :title="'Prógrömmin mín'" :action="toggleMenu"></custom-toolbar>      
      test
    </v-ons-page>
    
</template>

<script>
  import customToolbar from './toolbar'
  export default {
    props: ['toggleMenu'],
    components: { customToolbar }
  }
</script>
