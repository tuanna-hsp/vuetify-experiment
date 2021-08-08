<template>
  <div />
</template>

<script>
export default {
  props: {
    src: {
      type: String,
      required: true
    }
  },

  data() {
    return {
      audio: null,
      isReady: false
    };
  },

  mounted() {
    this.audio = new Audio("https://dotot.vn/sounds/empty.mp3");

    if (this.$device.isIos) {
      window.addEventListener("click", this.readyAudio);
    } else {
      this.isReady = true;
    }
  },

  beforeDestroy() {
    this.removeListeners();
    this.audio.pause();
  },

  methods: {
    removeListeners() {
      window.removeEventListener("click", this.readyAudio);
    },

    readyAudio() {
      this.audio.play();
      this.removeListeners();
      this.isReady = true;
    },

    play() {
      if (this.audio) {
        if (this.isReady && this.audio.src !== this.src) {
          this.audio.src = this.src;
        }

        this.audio.play().catch(_error => {});
      }
    },

    pause() {
      if (this.audio) {
        this.audio.pause();
      }
    },

    load() {
      if (this.audio) {
        this.audio.load();
      }
    }
  }
};
</script>
