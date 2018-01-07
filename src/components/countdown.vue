re<template> 
      <div>   
        <div>
            <img src="figure-0.png" class="figure" />
            <img src="images/figure-0.png" class="figure" />
            <img src="/images/figure-colon.png" />            
        </div>
        <v-ons-button modifier="large" @click="() => on ? stop() : start()" style="margin: 6px 0">{{ on ? 'Stopp' : 'Byrja' }}</v-ons-button>      
    </div>   
</template>

<script>  
  export default {
    props: ['startAt'],
    data() {
      return { 
        on: false,
        intervalId: null,
        value: this.startAt* 1000
      };
    }, 
    computed: {
      second() {
        const s = Math.floor(this.value/1000);
        return s >= 10 ? s : '0'+s;
      },
      millisecond() {
        const ms = Math.floor(this.value%10000)/100;
        return ms >= 10 ? ms : '0'+ms;
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
