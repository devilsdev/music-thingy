<template>
  <div class="soundbox">
        <input 
            type="checkbox" 
            v-model="isActive"  
            class="soundBox"
            :class="{active: isActive, isPlaying: isPlaying}"
        />
  </div>
</template>

<script>
export default {
  name: 'SoundBox',
  props: ['soundFile'],
  data () {
    return {
        isActive: false,
        isPlaying: false,
        sound: this.soundFile.sound
    }
  },
  watch: {
      isActive: function () {
          this.isActive ? new Audio(this.sound).play() : false
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
}
.active {
    background-color: var(--mainAccentColor);
}
.isPlaying {
    background-color: red;
}

*:focus {
    outline: none;
}
</style>