<template>
    <v-ons-page>
      <custom-toolbar :title="'Æfing 1'" :backLabel="'FRÍTT'" :action="toggleMenu"></custom-toolbar>
             
      <v-ons-carousel fullscreen swipeable auto-scroll overscrollable :index.sync="carouselIndex" :direction="'vertical'">
        <v-ons-carousel-item v-for="exercise in workout.exercises" :key="exercise.name">
          <component :is="countdown" :exercise="exercise" @done="carouselIndex += 1"></component>                
        </v-ons-carousel-item>
      </v-ons-carousel>
      
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
        carouselIndex: 0,
        countdown: countdown,
        workout: {
          name: 'Æfing 1',
          sets: 2,
          rest: 60,
          exercises: [{            
            name: 'Háhné',            
            reps: undefined,
            sets: 1,
            time: 5,
            rest: 10            
          },{
            name: 'Hnébeygjur',            
            reps: undefined,
            sets: 1,
            time: 15,
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