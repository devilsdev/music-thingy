<template>
  <div class="appGrid">
    <header class="header">
      <label for="bpmText">
        {{ bpm }} BPM 
      </label>
      <input type="range" min="30" max="200" class="slider" v-model="bpm">
    </header>


    <div class="musicLayout">
      <div class="musicGrid">
        <div v-for="index in 4" :key="index">
          <div v-for="sound in sounds" :key="sound.name">
            <sound-box soundFile="sound"></sound-box>
          </div>
        </div>
      </div>
    </div>

    <footer>
      <label> 
        <div class="playButton" @click="playSoundInRythm">
          <span v-if="isPlaying">||</span>
          <span v-else>></span>
          <span>Play/Pause</span>
        </div>
        
      </label>
    </footer>

  </div>
</template>

<script>
import SoundBox from './SoundBox'
export default {
  name: 'IntervalThing',
  components: {
    'sound-box': SoundBox
  },
  data () {
    return {
      currentSection: 0,
      sounds: {
        kick: {
          name: 'Kick',
          sound: require('./Kick 1.wav')
        },
        clap: {
          name: 'Clap',
          sound: require('./Clap 1.wav')
        },
        hat: {
          name: 'Hat',
          sound: require('./Open Hat 2.wav')
        },
        snare: {
          name: 'Snare',
          sound: require('./Snare 2.wav')
        }
      },
      sections: [
      ],
      title: 'Music Thing',
      bpm: 124,
      isPlaying: false,
      soundTimeOut: null
    }
  },
  computed: {
    rythmTime: function () {
      return (60 / this.bpm) * 1000
    },
  },
  methods: {
    playSoundInRythm () {
      this.isPlaying = !this.isPlaying
      if(!this.isPlaying) {
        console.log(this.currentSection)
        this.sections[this.currentSection].forEach(el => {
          if(el.checked)
            new Audio(el.sound).play()
        })
        this.currentSection += 1
        
        if(this.currentSection > 3)
          this.currentSection = 0
        this.soundTimeOut = setTimeout(this.playSoundInRythm, this.rythmTime)      
      }
    },
    stop () {
      this.isPlaying = false
      this.currentSection = 0
      clearTimeout(this.soundTimeOut)
    }
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

.playButton {
  cursor: pointer;
  user-select: none;
}
.playButton:hover{
  color: var(--mainAccentColor);
}
</style>
