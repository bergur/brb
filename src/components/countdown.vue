re<template> 
      <div>   
        <div style="text-align:center">                
          <img :src="numbers[0]" />
          <img :src="numbers[1]" />
          <img src="../images/figure-colon.png" />
          <img :src="numbers[2]" />
          <img :src="numbers[3]" />
        </div>        
        <v-ons-button modifier="large" @click="() => on ? stop() : start()" style="margin: 6px 0">{{ on ? 'Stopp' : 'Byrja' }}</v-ons-button>      
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
        on: false,
        intervalId: null,
        value: this.startAt* 1000,
        numbers: [figure0,figure1,figure2,figure3,figure4,figure5,figure6,figure7,figure8,figure9]
      };
    }, 
    computed: {
      time() {
        
      }      
    },
    methods: {
      start() {
        this.on = true  
        this.value = this.startAt * 1000;      
        this.intervalId = setInterval(() => {
          this.value -= 100;
          if (this.value === 0) {
              this.stop();
          }
        },100)
        
      },
      stop() {
        this.on = false;        
        clearInterval(this.intervalId);
      },
      clear() {
          this.value = 0;
      }      
    }    
  }
</script>
