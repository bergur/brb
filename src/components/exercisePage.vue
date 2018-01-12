<template>
    <v-ons-page>
      <custom-toolbar :title="'Æfing 1'" :backLabel="'FRÍTT'" :action="toggleMenu"></custom-toolbar>      
      <component :is="countdown" :exercise="workout.exercises[index]" :total="total"  @done="next" ></component>                              
            
    </v-ons-page>
    
</template>

<script>
  import customToolbar from './toolbar'
  import countdown from './countdown'
  export default {
    props: ['toggleMenu'],
    data() {    
      return {       
        index: 0,        
        countdown: countdown,
        finished: false,
        workout: {
          name: 'Æfing 1',
          sets: 2,
          rest: 60,
          exercises: [{            
            name: 'Háhné',            
            reps: undefined,            
            time: 2,
            rest: 3                                  
          },{
            name: 'Hnébeygjur',            
            reps: undefined,
            time: 2,
            rest: 3
          },{
            name: 'Burpees',            
            reps: undefined,            
            time: 2,
            rest: 3
          },{
            name: 'Framstig',            
            reps: undefined,            
            time: 2,
            rest: 3
          },{
            name: 'Gangandi armbegyjur',            
            reps: undefined,            
            time: 2,
            rest: 3
          }]
        }
      };
    },    
    computed: {
      total() {
        return this.workout.exercises.reduce((t,i) => t + (i.time+i.rest),0);
      }
    },
    methods: {
      next() {
        if (this.index +1 < this.workout.exercises.length)
        {
          this.index +=1;
          this.finished=false;
        }        
        else {
          this.finished=true;
        }
      }
    },
    components: { customToolbar, countdown }
  }
</script>