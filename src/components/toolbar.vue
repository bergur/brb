<template id="toolbar">
    <v-ons-toolbar>      
      <div class="left">
        <v-ons-back-button :on-click="pop">{{ backLabel }}</v-ons-back-button>
      </div>
      <div class="center">{{ title }}</div>
      <div class="right">
        <v-ons-toolbar-button @click="action">
          <v-ons-icon icon="ion-navicon, material:md-menu"></v-ons-icon>
        </v-ons-toolbar-button>
      </div>
    </v-ons-toolbar>
</template>

<script>
  export default {
    props: ['title', 'action', 'pop','backLabel']
  } 
</script>
