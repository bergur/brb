<template>
    <v-ons-page>
      <custom-toolbar :title="'Prógrömmin mín'" :action="toggleMenu"></custom-toolbar>      
      <v-ons-list>
        <v-ons-list-item modifier="chevron" tappable @click="push">
          <div class="list-item__title">
            FRÍTT            
          </div>
          <div class="list-item__subtitle">
            Einfaldar æfingar sem hægt er að gera hvar sem er.
          </div>
        </v-ons-list-item >
        <v-ons-list-item modifier="chevron" tappable>
          <div class="list-item__title">
            Styrkur #1
          </div>
          <div class="list-item__subtitle">
            Æfingar í tækjum til að byggja upp grunnstyrk.
          </div>
        </v-ons-list-item>
        <v-ons-list-item modifier="chevron" tappable>
          <div class="list-item__title">
            Þrekhringur #3
          </div>
          <div class="list-item__subtitle">
            Mikil ákefð og stuttar hvíldir.
          </div>
        </v-ons-list-item>
      </v-ons-list>
    </v-ons-page>    
</template>

<script>
  import customToolbar from './toolbar'
  import program from './programPage'
  
  export default {
    props: ['toggleMenu'],    
    components: { customToolbar },
    methods: {      
      push() {
        console.log('inn');
        this.$emit('push-page', program);        
      }      
    }
  }
</script>
