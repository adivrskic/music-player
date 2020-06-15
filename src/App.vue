<template>
  <div id="app">
    <header :class="{'blur': showModal}">
      <div class="content">
        <Logo />
        <h1>{{ appTitle }}</h1>
      </div>
    </header>
    <Tracklist :tracks="tracks" :class="{'blur': showModal}"/>
    <TrackModal v-if="showModal" :track="track" />
  </div>
</template>

<script>
import Logo from './assets/images/Logo'
import Tracklist from './components/Tracklist'
import TrackModal from './components/TrackModal'

import { eventBus } from './main.js'

export default {
  name: 'App',
  data() {
    return {
      appTitle: 'My Music',
      showModal: false,
      track: '',
      tracks: [
        {
          title: 'Aurora',
          artist: 'Jacoo',
          image: require('./assets/songs/jacoo/image/jacoo.jpg'),
          src: require('./assets/songs/jacoo/aurora.mp3')
        },
        {
          title: 'Memories',
          artist: 'Jacoo',
          image: require('./assets/songs/jacoo/image/jacoo.jpg'),
          src: require('./assets/songs/jacoo/memories.mp3')
        },
        {
          title: 'Redemption',
          artist: 'Blackmill',
          image: require('./assets/songs/blackmill/image/blackmill.jpg'),
          src: require('./assets/songs/blackmill/redemption.mp3')
        },
        {
          title: 'One Kingdom',
          artist: 'Killigrew',
          image: require('./assets/songs/killigrew/image/killigrew.jpg'),
          src: require('./assets/songs/killigrew/one_kingdom.mp3')
        },
        {
          title: 'Kida',
          artist: 'Killigrew',
          image: require('./assets/songs/killigrew/image/killigrew.jpg'),
          src: require('./assets/songs/killigrew/kida.mp3')
        }
      ]
    }
  },
  components: {
    Logo,
    Tracklist,
    TrackModal
  },
  created() {
    eventBus.$on('playTrack', data => {
      console.log(data)
      this.track = data
      this.showModal = true;
    }),
    eventBus.$on('closeModal', () => {      
      this.showModal = false;
    })
  }
}
</script>

<style>
html, body {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}

header {
  background-color: #42378f;
  background-image: linear-gradient(315deg, #42378f 0%, #f53844 74%);
}

header .content {
  display: flex;
  justify-content: space-between;
  align-items: center;
  color: #fff;
  padding: 1.5rem;
}

.content {
  max-width: 1080px;
  margin: 0 auto;
}

header svg {
  width: 4rem;
}

header h1 {
  font-size: 2.5rem;
  text-transform: uppercase;
  letter-spacing: .25rem;
  margin: 0;
}

.blur {
  filter: blur(4px);
}

@media screen and (max-width: 480px) {
  header h1 {
    display: none;
  }

  header .content {
    justify-content: center;
  }
}
</style>
