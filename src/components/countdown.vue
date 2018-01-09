re<template> 
      <div>   
        <div style="text-align:center">                
          <img :src="numbers[minutes.ten]" />
          <img :src="numbers[minutes.unit]" />
          <img src="../images/figure-colon.png" />
          <img :src="numbers[seconds.ten]" />
          <img :src="numbers[seconds.unit]" />
          <img src="../images/figure-colon.png" />
          <img :src="numbers[hundreds.ten]" />
          <img :src="numbers[hundreds.unit]" />          
        </div>                
        <v-ons-button modifier="large" @click="() => !running  ? start() : stop()" style="margin: 6px 0">{{  !running ? 'Byrja' : 'Stopp' }}</v-ons-button>      
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
    props: ['startAt', 'next'],
    
    data() {
      return { 
        running: false,
        intervalId: null,
        value: this.startAt* 100,
        numbers: [figure0,figure1,figure2,figure3,figure4,figure5,figure6,figure7,figure8,figure9]
      };
    }, 
    computed: {  
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
      start() {
        this.running = true;
        this.intervalId = setInterval(() => {
          this.value -= 1;
          if (this.value === 0) {                            
              this.stop();
              this.$emit('next', 'bergur');
          }
        },10)
        
      },
      stop() {
        this.running = false;
        clearInterval(this.intervalId);
      },
      clear() {
          this.value = 0;
      }      
    }    
  }
</script>
