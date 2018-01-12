<template> 
      <div>     
          <v-ons-progress-bar :value="progress"></v-ons-progress-bar>      
          <div style="text-align:center">
            <div style="font-size:48px; text-align:center; margin: 16px 0 16px 0; text-transform: uppercase">{{ title }}</div>                
            <img :src="numbers[minutes.ten]" width="50" height="75" />
            <img :src="numbers[minutes.unit]" width="50" height="75" />
            <img src="../images/figure-colon.png" width="25" height="75" />
            <img :src="numbers[seconds.ten]" width="50" height="75" />
            <img :src="numbers[seconds.unit]" width="50" height="75" />
            <img src="../images/figure-colon.png" width="25" height="75" />
            <img :src="numbers[hundreds.ten]" width="50" height="75" />
            <img :src="numbers[hundreds.unit]" width="50" height="75" />  
            
            <v-ons-button modifier="large" @click="click" style="margin-top: 16px">{{  !running ? 'Byrja' : 'Stopp' }}</v-ons-button>      
          </div>

    </div>   
</template>

<script>
  import figurec from '../images/figure-0.png';
  import figure0 from '../images/figure-0.png';
  import figure1 from '../images/figure-1.png';
  import figure2 from '../images/figure-2.png';
  import figure3 from '../images/figure-3.png';
  import figure4 from '../images/figure-4.png';
  import figure5 from '../images/figure-5.png';
  import figure6 from '../images/figure-6.png';
  import figure7 from '../images/figure-7.png';
  import figure8 from '../images/figure-8.png';
  import figure9 from '../images/figure-9.png';

  export default {
    props: {
      exercise: Object,      
      total: Number
    },
    data() {
      return {       
        sum: 0,                  
        running: false,                
        intervalId: null,
        value: this.exercise.time * 100,
        title: this.exercise.name,
        numbers: [figure0,figure1,figure2,figure3,figure4,figure5,figure6,figure7,figure8,figure9]
      };
    },        
    computed: {
      progress() {
        console.log(this.sum);
        return Math.floor(this.sum/this.total);
      },
      minutes() {
        let minutes = Math.floor(this.value/6000);
        return {
          ten: (minutes >= 10) ? Math.floor(minutes/10) : 0, 
          unit: (minutes >= 10) ? Math.floor(minutes%10) : minutes
        };
      },         
      seconds() {
        let seconds = Math.floor(this.value%6000/100)                
        
        return {
          ten: (seconds >= 10) ? Math.floor(seconds/10) : 0,
          unit: (seconds >= 10) ? Math.floor(seconds%10) : seconds
        };
      },
      hundreds() {
        let hundreds = Math.floor(this.value%6000%100)
        
        return {
          ten: (hundreds >= 10) ? Math.floor(hundreds/10) : 0,
          unit: (hundreds >= 10) ? Math.floor(hundreds%10) : hundreds
        }
      }      
    },          
    methods: {   
      click() {
        if (this.running) {
          this.stop();
        }
        else {        
          this.startExercise();
        }
      },
      countdown(cb) {   
        setTimeout(() => {       
          this.running = true;        
          this.intervalId = setInterval(() => {
            this.sum += 1;
            console.log(this.sum);
            this.value -= 1;            
            if (this.value === 0) {                                                    
              this.stop();               
              cb();
            }
          },10)                  
        },1000);
      },    
      startExercise() {                 
        this.title = this.exercise.name;  
        this.value = this.exercise.time * 100                                 
        this.countdown(() => {          
          setTimeout(this.startRest,500)
        });
      },
      startRest() {           
        this.resting = true;     
        this.title = 'HVÍLD';
        this.value = this.exercise.rest * 100;        
        this.countdown(()  => {              
          this.$emit('next');                       
          
          if (this.progress !== 100) {            
            setTimeout(this.startExercise,500);             
          }          
          else {
            this.$emit('finished');
          }
        });                        
      },
      stop() {
        this.running = false;        
        clearInterval(this.intervalId);
      }         
    }    
  }
</script>

<style>
  .fade-enter-active, .fade-leave-active {
    transition: opacity 0;  
  }
  
  .fade-enter, .fade-leave-to /* .fade-leave-active below version 2.1.8 */ {
    opacity: .5s;
  }
</style>