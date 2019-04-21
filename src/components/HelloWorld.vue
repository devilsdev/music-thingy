<template>
  <div class="hello">
    <h1>{{ title }}</h1>
    <label for="slider">BPM: {{ bpm }}</label> <br/>
    <input name="slider" type="range" min="1" max="200" v-model="bpm"> <br/>
    <button @click="play">Play</button>
    <button @click="stop">Stop</button>

  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
      title: 'Music Thing',
      bpm: 124,
      isPlaying: false,
      intervalPlaying: null
    }
  },
  computed: {
    rythmTime: () => {
      console.log(this.bpm)  
      return (60 / this.bpm) * 1000
    }
  },
  methods: {
    play () {
      if(this.isPlaying == false) {
        this.isPlaying = true
        // play the first one
        new Audio(require('./Kick 1.wav')).play()

        let test
        this.intervalPlaying = setInterval(() => {
          test = new Audio(require('./Kick 1.wav')).play()
        }, this.rythmTime)

      }
    },
    stop () {
      this.isPlaying = false
      clearInterval(this.intervalPlaying)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
