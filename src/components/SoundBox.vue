<template>
  <div class="soundbox">
        <input 
            type="checkbox" 
            v-model="sound.isActive"  
            class="soundBox"
            :class="{isActive: sound.isActive, isPlayed: sound.isPlayed}"
            @change="this.fireEvent"
        />
  </div>
</template>

<script>
export default {
  name: 'SoundBox',
  props: ['soundFile'],
  data () {
    return {
        sound: this.soundFile
    }
  },
  methods: {
    fireEvent (event) {
      this.$emit('fireEvent', this.sound)
      console.log(this.sound)
    } 
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.soundBox {
  width: 5rem;
  height: 5rem;
  appearance: none;
  background-color: #989898;
  border: 1px solid ;
  border-radius: 3px;
  border-style: none;
  cursor: pointer;
}
.isActive {
    background-color: var(--mainAccentColor);
}
.isPlayed {
    background-color: #f25400;
}

*:focus {
    outline: none;
}
</style>