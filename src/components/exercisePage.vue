<template>
    <v-ons-page>
      <custom-toolbar :title="'Æfing 1'" :backLabel="'FRÍTT'" :action="toggleMenu"></custom-toolbar>

      <component :is="countdown" :exercise="workout.exercises[index]" :finished="finished"  @done="next" ></component>                              
      
      <div style="width:100%; text-align:center; margin-top:20px">
        <span v-for="(exercise,i) in workout.exercises" :key="exercise.name">
          <span :style="{ width: Math.floor(exercise.time/total*100) + '%', backgroundColor: i == index ? 'red' : 'blue' }" style="display:block; color:#fff; float:left;">&nbsp;</span>
          <span :style="{ width: Math.floor(exercise.rest/total*100) + '%', backgroundColor: i == index ? 'red' : 'grey' }" style="display:block; color:#000; float:left;">&nbsp;</span>
        </span>
      </div>
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