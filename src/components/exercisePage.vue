<template>
    <v-ons-page>
      <custom-toolbar :title="'Æfing 1'" :backLabel="'FRÍTT'" :action="toggleMenu"></custom-toolbar>
      <countdown startAt="5" :startAt="workout.exercises[current].time" @bergur="done"></countdown>           
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
        current: 0,
        workout: {
          name: 'Æfing 1',
          sets: 2,
          rest: 60,
          exercises: [{
            name: 'Háhné',
            reps: undefined,
            sets: 1,
            time: 15,
            rest: 10
          },{
            name: 'Hnébeygjur',
            reps: undefined,
            sets: 1,
            time: 5,
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
      done() {
        console.log('jei');

        if (this.current < this.workout.exercises.length) {
          this.current += 1;
        }
      },
      push() {
        this.$emit('push-page', exercise);
      }      
    },
    components: { customToolbar, countdown }
  }
</script>