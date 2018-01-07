<template>
    <v-ons-page>
      <custom-toolbar :title="'Æfing 1'" :backLabel="'FRÍTT'" :action="toggleMenu"></custom-toolbar>
      <countdown startAt="30"></countdown>           
    </v-ons-page>
    
</template>

<script>
  import customToolbar from './toolbar'
  import countdown from './countdown'
  import exercise from './exercisePage'
  export default {
    props: ['toggleMenu'],
    data() {
      return {                
        workout: {
          name: 'Æfing 1',
          sets: 2,
          rest: 60,
          exercises: [{
            name: 'Háhné',
            reps: undefined,
            sets: 1,
            time: 30,
            rest: 10
          },{
            name: 'Hnébeygjur',
            reps: undefined,
            sets: 1,
            time: 30,
            rest: 10
          },{
            name: 'Burpees',
            reps: undefined,
            sets: 1,
            time: 30,
            rest: 10
          },{
            name: 'Framstig',
            reps: undefined,
            sets: 1,
            time: 30,
            rest: 10
          },{
            name: 'Gangandi armbegyjur',
            reps: undefined,
            sets: 1,
            time: 30,
            rest: 10
          }]
        }
      };
    },     
    methods: {      
      push() {
        this.$emit('push-page', exercise);
      }      
    },
    components: { customToolbar, countdown }
  }
</script>