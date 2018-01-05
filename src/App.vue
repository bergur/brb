<template>
  <v-ons-splitter>
    <v-ons-splitter-side
      swipeable width="150px" collapse="" side="left"
      :open.sync="openSide"
    >
      <v-ons-page>
        <v-ons-list>
          <v-ons-list-header>Menu</v-ons-list-header>
          <v-ons-list-item v-for="page in pages" :key="page" tappable modifier="chevron" @click="currentPage = page; openSide = false">
            <div class="center">{{ page }}</div>
          </v-ons-list-item>
        </v-ons-list>
      </v-ons-page>
    </v-ons-splitter-side>

    <v-ons-splitter-content>
      <v-ons-navigator :page-stack="pageStack">
        <component v-for="page in pageStack" :is="page" :key="page" @push="pageStack.push($event)"></component>
      </v-ons-navigator>
      <div :is="currentPage" :toggle-menu="() => openSide = !openSide"></div>
    </v-ons-splitter-content>
  </v-ons-splitter>
</template>

<script>
  import home from './components/homePage'
  import program from './components/programPage'
  import news from './components/newsPage'
  import settings from './components/settingsPage'
  export default {
    data() {
      return {
        currentPage: 'home',
        pages: ['home', 'news', 'settings'],
        pageStack: ['home'],
        openSide: false
      };
    },    
    components: {
      home,
      news,
      settings
    }
  }
</script>
