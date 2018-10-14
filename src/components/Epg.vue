<template>
  <div class="epg-layout">
    <button class="now" @click.prevent="scrollCurrent">NOW</button>
    <div class="timeline">
      <div class="channels">
        <div class="channel" v-for="(channel, c) in channels" :key="c">
          <img :src="channel.images.logo" :alt="channel.title">
        </div>
      </div>
      <div class="movies-body" ref="scrollable">
        <div class="movies timebar">
          <div class="movie" v-for="h in 24" :key="h"><span class="pos" v-if="currentTime.getHours() == h - 1" :style="{ left: position + 'px' }"></span><em>{{ h - 1 }}:00</em></div>
        </div>
        <div class="movies" v-for="(channel, k) in channels" :key="k">
          <span class="mpos" :style="{ left: mposition + 'px' }"></span>
          <div class="movie" v-for="(movie, m) in channel.schedules" :key="m" :class="{ active: isActive(movie) }" :style="{ minWidth: calculateWidth(movie) + 'px' }">
            <div class="title">{{ movie.title }}</div>
            <p>{{ movie.start | time }} - {{ movie.end | time }}</p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {

  props: ['channels'],

  data() {
    return {
      position: 0,
      mposition: 0,
      currentTime: new Date,
    }
  },

  mounted() {
    this.position = this.currentTime.getMinutes() * 6
    this.mposition = this.currentTime.getHours() * 360 + 102 + this.position
    this.scrollCurrent()
  },

  filters: {
    time: (date) => {
      let d = new Date(date)
      return d.toLocaleTimeString({}, { hour12: false, hour: "2-digit", minute: "2-digit" })
    }
  },

  methods: {
    calculateWidth(movie) {
      var diff = Math.abs(new Date(movie.start) - new Date(movie.end));
      var minutes = Math.floor((diff/1000)/60);
      return minutes * 6;
    },

    isActive(movie) {
      let d1 = new Date(movie.start).getTime();
      let d2 = new Date(movie.end).getTime();

      if ( this.currentTime >= d1 && this.currentTime < d2 ) {
        return true
      }

      return false
    },

    scrollCurrent() {
      let scroll = this.currentTime.getHours() * 360 + this.currentTime.getMinutes() * 6 - 100
      this.$refs.scrollable.scroll({ left: scroll, behavior: 'smooth' })
    }
  }

};
</script>

<style scoped>
  .epg-layout { position: relative; }
  .timeline { display: grid; background-color: #202020; }
  .channels { background-color: #202020; width: 100px; position: absolute; top: 49px; z-index: 5; }
  .channels .channel:first-of-type { border-top: 1px solid #515151; }
  .movies-body::-webkit-scrollbar-track {-webkit-box-shadow: inset 0 0 6px rgba(0,0,0,0.3); border-radius: 10px; background-color: transparent; } .movies-body::-webkit-scrollbar {height: 4px; width: 8px; background-color: transparent; } .movies-body::-webkit-scrollbar-thumb {border-radius: 10px; -webkit-box-shadow: inset 0 0 6px rgba(0,0,0,.3); background-color: rgba(255, 255, 255, .2); }
  .movies-body { overflow-x: auto; background-color: #111111; }
  .movies { display: flex; position: relative; padding-left: 100px; }
  .channel { display: flex; width: 100px; height: 79px; color: #545454; border-bottom: 1px solid #515151; align-items: center; justify-content: center; box-shadow: 20px 0px 20px -20px rgba(0, 0, 0, 0.8); }
  .channel img { width: 40px; }
  .movie { box-sizing: border-box; text-align: center; color: #545454; height: 80px; display: flex; flex-direction: column; justify-content: center; font-size: 85%; border-left: 1px solid #515151; }
  .movie:last-of-type { border-right: 1px solid #515151; }
  .movie .title { color: #fff; }
  .movie p { margin: 0; font-size: 75%; margin-top: 5px; color: #b3b3b3; }
  .movie.active { background-color: #393939; }
  .movies:after { content: ''; display: block; height: 1px; left: 0; width: 8740px; bottom: 0; background-color: #515151; position: absolute; }
  .timebar div { min-width: 240px; color: #fff; }
  .timebar .movie em { left: -17px; display: inline-block; position: relative; font-style: normal; font-size: 110%; }
  .timebar .movie:after { content: ''; display: block; height: 10px; width: 1px; left: 0; background-color: rgba(255, 255, 255, .3); bottom: 0; position: absolute; }
  .channel.timebar { opacity: 0; height: 30px; }
  .movies.timebar .movie { height: 50px; text-align: left; position: relative; min-width: 360px; border: 0; }
  .movies.timebar { background-color: #202020; }
  .timebar .pos { display: block; top: 5px; width: 5px; height: 32px; margin: 4px 0; position: absolute; background-color: #e1a21e; border-radius: 2px; }
  .mpos {display: block; top: -10px; bottom: 0; width: 1px; background: #e1a21e; position: absolute; left: 0px; }
  .now { position: fixed; right: 20px; bottom: 60px; color: #fff; background-color: #e1a21e; border: 0; padding: 10px; min-width: 80px; border-radius: 5px; z-index: 10; transition-duration: .3s; cursor: pointer; }
  .now:hover { background-color: #bd891b; }
</style>
