<template>
    <v-ons-page>
      <custom-toolbar :title="'FRÍTT'" backLabel="Prógrömmin mín" :action="toggleMenu"></custom-toolbar>                  
      <v-ons-carousel fullscreen swipeable auto-scroll overscrollable :index.sync="carouselIndex">
      <v-ons-carousel-item v-for="item in items"> 
        <v-ons-card>      
          <div class="title">Æfing #{{ item.key }}</div>
          <div class="content">
            <div style="margin-bottom: 16px">{{ item.description }}</div>
          
            <v-ons-list>      
              <v-ons-list-header>Æfingar</v-ons-list-header>                  
              <v-ons-list-item>Há hné</v-ons-list-item>
              <v-ons-list-item>Hnébeygjur</v-ons-list-item>
              <v-ons-list-item>Burpees</v-ons-list-item>
              <v-ons-list-item>Framstig</v-ons-list-item>
              <v-ons-list-item>Gangandi armbeygjur</v-ons-list-item> 
            </v-ons-list>

            <v-ons-button modifier="large" @click="push" style="margin: 6px 0">Velja</v-ons-button>
        </div>
      </v-ons-card>                 
      </v-ons-carousel-item>
    </v-ons-carousel>

    <div :style="dots">
      <span :index="dotIndex - 1" v-for="dotIndex in Object.keys(items).length" :key="dotIndex" style="cursor: pointer" @click="carouselIndex = dotIndex - 1">
        {{ carouselIndex === dotIndex - 1 ? '\u25CF' : '\u25CB' }}
      </span>
    </div>        
    </v-ons-page>
    
</template>

<script>
  import customToolbar from './toolbar'
  import exercise from './exercisePage'
  export default {
    props: ['toggleMenu'],
    data() {
      return {
        carouselIndex: 0,
        items: [
          {
            key: 1,
            description: 'Þetta er svokölluð HIIT æfing. Þú framkvæmir æfingu í 30 sek og hvílir svo í 10 sek. Æfingarnar eru 6 talsins. Eftir hverja umferð er 1 min hvíld'
          },
          {
            key: 2,
            description: 'Þetta er svokölluð HIIT æfing. Þú framkvæmir æfingu í 30 sek og hvílir svo í 10 sek. Æfingarnar eru 6 talsins. Eftir hverja umferð er 1 min hvíld'
          },
          {
            key: 3,
            description: 'Þetta er svokölluð HIIT æfing. Þú framkvæmir æfingu í 30 sek og hvílir svo í 10 sek. Æfingarnar eru 6 talsins. Eftir hverja umferð er 1 min hvíld'
          }
        ],
        dots: {
          textAlign: 'center',
          fontSize: '30px',
          color: '#000',
          position: 'absolute',
          bottom: '40px',
          left: 0,
          right: 0
        }
      };
    },
    methods: {
      push() {
        this.$emit('push-page', exercise);        
      }      
    },
    components: { customToolbar }
  }
</script>
