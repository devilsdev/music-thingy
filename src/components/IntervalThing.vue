<template>
  <div class="hello">
    <h1>{{ title }}</h1>
    <label for="slider">BPM: {{ bpm }}</label> <br/>
    <input name="slider" type="range" min="1" max="200" v-model="bpm"> <br/>
    <button @click="playSoundInRythm">Play</button>
    <button @click="stop">Stop</button>

    <div v-for="section in sections" :key="section" style="display: flex;">
      <div v-for="sound in section" :key="sound.name" >
          {{ sound.name }} : <input type="checkbox" v-model="sound.checked" />
      </div>
    </div>



  </div>
</template>

<script>
import SoundThing from './SoundThing'
export default {
  name: 'IntervalThing',
  components: {
    'sound-thing': SoundThing
  },
  data () {
    return {
      currentSection: 0,
      sections: [
        [
          {
            name: 'Kick',
            sound: require('./Kick 1.wav'),
            checked: false
          },
          {
            name: 'Clap',
            sound: require('./Clap 1.wav'),
            checked: false
          },
          {
            name: 'Kick2',
            sound: require('./Kick 1.wav'),
            checked: false
          },
          {
            name: 'Clap2',
            sound: require('./Clap 1.wav'),
            checked: false
          }
        ], [
          {
            name: 'Kick',
            sound: require('./Kick 1.wav'),
            checked: false
          },
          {
            name: 'Clap',
            sound: require('./Clap 1.wav'),
            checked: false
          },
          {
            name: 'Kick2',
            sound: require('./Kick 1.wav'),
            checked: false
          },
          {
            name: 'Clap2',
            sound: require('./Clap 1.wav'),
            checked: false
          }
        ], [
          {
            name: 'Kick',
            sound: require('./Kick 1.wav'),
            checked: false
          },
          {
            name: 'Clap',
            sound: require('./Clap 1.wav'),
            checked: false
          },
          {
            name: 'Kick2',
            sound: require('./Kick 1.wav'),
            checked: false
          },
          {
            name: 'Clap2',
            sound: require('./Clap 1.wav'),
            checked: false
          }          
        ], [
          {
            name: 'Kick',
            sound: require('./Kick 1.wav'),
            checked: false
          },
          {
            name: 'Clap',
            sound: require('./Clap 1.wav'),
            checked: false
          },
          {
            name: 'Kick2',
            sound: require('./Kick 1.wav'),
            checked: false
          },
          {
            name: 'Clap2',
            sound: require('./Clap 1.wav'),
            checked: false
          }          
        ]
        
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
      clearTimeout(this.soundTimeOut)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}

.diese {
  display: flex;
}

input[type="checkbox"] {
  width: 50px;
  height: 50px;
}
</style>
