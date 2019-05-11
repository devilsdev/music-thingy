<template>
  <div class="appGrid">
    <header class="header">
      <label for="bpmText">
        {{ bpm }} BPM 
      </label>
      <input type="range" min="30" max="200" class="slider" v-model="bpm">
    </header>

    <main class="musicLayout">
      <div class="musicGrid">
        <div v-for="(section, index) in sections" :key="index">
          <div v-for="(sound, index) in section" :key="index">
            <sound-box 
              :soundFile="sound" 
              @fireEvent="sound = $event"
            />
          </div>
        </div>
      </div>
    </main>

    <footer>
      <label> 
        <div class="playStopButton">
          <span v-if="isPlaying" @click="stop">|| Pause</span>
          <span v-else @click="playSoundInRythm">> Play</span>
        </div>
      </label>
    </footer>

  </div>
</template>

<script>
import _ from 'lodash'; 
import SoundBox from './SoundBox'

export default {
  name: 'IntervalThing',
  components: {
    'sound-box': SoundBox
  },
  data () {
    return {
      sounds: [
        {
          id: null,
          name: 'Kick',
          sound: require('./Kick 1.wav'),
          isActive: false,
          isPlayed: false
        },
        {
          id: null,
          name: 'Clap',
          sound: require('./Clap 1.wav'),
          isActive: false,
          isPlayed: false
        },
        {
          id: null,
          name: 'Hat',
          sound: require('./Open Hat 2.wav'),
          isActive: false,
          isPlayed: false
        },
        {
          id: null,
          name: 'Snare',
          sound: require('./Snare 2.wav'),
          isActive: false,
          isPlayed: false
        }
      ],
      title: 'Music Thing',
      bpm: 124,
      isPlaying: false,
      soundTimeOut: null,
      currentSection: 0,
      sections: []
    }
  },
  computed: {
    rythmTime: function () {
      return (60 / this.bpm) * 1000
    }
  },
  methods: {
    playSoundInRythm () {
      this.isPlaying = true

      if(this.currentSection > 3)
        this.currentSection = 0
      
      let currentSounds = this.sections[this.currentSection]
      currentSounds.forEach(sound => {
        if(sound.isActive) {
          sound.isPlayed = true
          new Audio(sound.sound).play()
          setTimeout(() => sound.isPlayed = false, 130)
        }

      })

      this.currentSection++
      this.soundTimeOut = setTimeout(this.playSoundInRythm, this.rythmTime) 
    },
    stop () {
      this.isPlaying = false
      this.currentSection = 0
      clearTimeout(this.soundTimeOut)
    },
    createSections () {
      // create 4 sections of the sounds array
      // each one has to be a deep clone of the array
      // for this, we will use lodash
      // i will refactor this later (sure i will ... :))
      const sec1 = [...this.sounds]
      let copy1 = _.map(this.sounds, _.clone)
      let copy2 = _.map(this.sounds, _.clone);
      let copy3 = _.map(this.sounds, _.clone);
      let copy4 = _.map(this.sounds, _.clone);
      copy1.forEach(sound => sound.id = Math.random())
      copy2.forEach(sound => sound.id = Math.random())
      copy3.forEach(sound => sound.id = Math.random())
      copy4.forEach(sound => sound.id = Math.random())
      this.sections.push(copy1, copy2, copy3, copy4)
    }
  },
  mounted () {
    this.createSections()
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.appGrid {
  height: 100vh;
  display: grid;
  grid-template-rows: repeat(8, 1fr);
  grid-template-columns: repeat(6, 1fr);
  
  align-items: start;
}

.header {
  width: 100%;
  height: 100%;
  grid-column-start:2; 
  grid-column-end:2; 
  grid-row-start:1; 
  grid-row-end:1; 
  text-align: left;
  font-size: 37px;
  word-spacing: 5px;
  font-weight: bold;
}

.header > label {
  width: 100%;
}

.slider {
  grid-column-start:2; 
  grid-column-end:6; 
  grid-row-start:3; 
  grid-row-end:6; 

  -webkit-appearance: none;  
  appearance: none;
  width: 40vw; 
  height: 25px; 
  background: var(--mainAccentColor); 
  outline: none;
  opacity: 0.5;
  -webkit-transition: .2s;
  transition: opacity .2s;
}

.slider:hover {
  opacity: 1;
}

.slider::-webkit-slider-thumb {
  -webkit-appearance: none; 
  appearance: none;
  width: 25px; 
  height: 25px; 
  background: var(--mainBgColor); 
  cursor: pointer; 
  opacity: 0.5;
}

.musicLayout {
  grid-column-start:2; 
  grid-column-end:6; 
  grid-row-start:3; 
  grid-row-end:6; 
}

.musicGrid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  align-items: start;
}

footer {
  grid-column-start:2; 
  grid-column-end:6; 
  grid-row-start:7; 
  grid-row-end:7; 
  text-align: left;
  font-size: 37px;
}

.playStopButton {
  cursor: pointer;
  user-select: none;
}

.playButton:hover{
  color: var(--mainAccentColor);
}
</style>
