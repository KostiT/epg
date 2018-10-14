<template>
  <div id="app">
    <Header />
    <Timeline />
    <Epg :channels="entries" />
    <Footer />
  </div>
</template>

<script>
// main component.
import Epg from './components/Epg.vue'

import Header from './components/Header.vue'
import Footer from './components/Footer.vue'
import Timeline from './components/Timeline.vue'

export default {
  name: 'app',
  components: {
    Epg,
    Header,
    Timeline,
    Footer,
  },

  data() {
    return {
      entries: []
    }
  },

  mounted() {
    fetch('http://localhost:1337/epg')
    .then(r => r.json())
    .then(r => this.entries = r.channels)
  }
};
</script>

<style>

</style>
