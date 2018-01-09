re<template> 
      <div>           
          <div style="text-align:center">                
            <img :src="numbers[0]" />
            <img :src="numbers[1]" />
            <img src="../images/figure-colon.png" />
            <img :src="numbers[0]" />
            <img :src="numbers[1]" />
            <img src="../images/figure-colon.png" />
            <img :src="numbers[2]" />
            <img :src="numbers[3]" />
          </div>        
          <transition name="fade">
            <span v-show="show">{{ value }}</span>
          </transition>
          <v-ons-button modifier="large" @click="() => running ? stop() : start()" style="margin: 6px 0">{{ running ? 'Stopp' : 'Byrja' }}</v-ons-button>      
        
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
    props: ['startAt'],
    data() {
      return { 
        show: true,
        running: false,
        intervalId: null,
        value: this.startAt* 100,
        numbers: [figure0,figure1,figure2,figure3,figure4,figure5,figure6,figure7,figure8,figure9]
      };
    }, 
    watch: {      
      startAt(newVal) { 
        this.show = false;       
        setTimeout(() => {
          this.show = true;
          this.value = newVal * 100;
          this.start();
        },1500)
        
        
      }
    },
    methods: {
      start() {
        this.running = true                   
        this.intervalId = setInterval(() => {
          this.value -= 1;
          if (this.value === 0) {
              this.$emit('bergur',true)
              this.stop();
          }
        },10)
        
      },
      stop() {
        this.running = false;         
        clearInterval(this.intervalId);
      },
      clear() {
          this.value = this.startAt* 100;
      }      
    }    
  }
</script>
<style>
  .fade-enter-active, .fade-leave-active {
    transition: opacity .5s;
  }
  
  .fade-enter, .fade-leave-to /* .fade-leave-active below version 2.1.8 */ {
    opacity: 0;
  }
</style>