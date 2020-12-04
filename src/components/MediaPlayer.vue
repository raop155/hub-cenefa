<template>
  <div id="mediaPlayer">
    <video
      ref="videoRef"
      :src="src"
      type="video/mp4"
      autoplay
      muted
      @ended="onEnd()"
    >
      Your browser does not support HTML5 video.
    </video>
  </div>
</template>

<script>
export default {
  name: 'MediaPlayer',
  data: () => {
    return {
      src: null,
      index: 0,
      playlist: [
        //require('@/assets/01 FADE.mp4'),
        require('@/assets/01.mp4')
        //require('@/assets/01.mp4'),
        //require('@/assets/01.mp4'),
        //require('@/assets/01 FADE.mp4'),
        //require('@/assets/02 FADE.mp4'),
        //require('@/assets/02.mp4'),
        //require('@/assets/02.mp4'),
        //require('@/assets/02.mp4'),
        //require('@/assets/02 FADE.mp4')
        // require('@/assets/01 FULL.mp4')
      ]
    };
  },
  mounted() {
    var videoURL = this.playlist[this.index];
    console.log('videoURL >>', videoURL, 'index >>', this.index);
    this.src = videoURL;
    //this.$refs.videoRef.load();
    //this.$refs.videoRef.pause();
    //this.$refs.videoRef.play();

    this.index++;

    console.log('this.$refs.videoRef', this.$refs.videoRef);
    //this.$refs.videoRef.pause();
    //this.$refs.videoRef.currentTime = 0;
  },
  methods: {
    onEnd: function() {
      //this.$refs.videoRef.currentTime = 1;

      console.log('MediaPlayer Video Ended!');

      if (this.index == this.playlist.length) {
        this.index = 0;
      }

      var videoURL = this.playlist[this.index];
      console.log('videoURL >>', videoURL, 'index >>', this.index);

      if (videoURL == this.src) {
        console.log('Same video!');
        this.$refs.videoRef.currentTime = 0;
        this.$refs.videoRef.play();
      } else {
        console.log('Different video!');
        this.src = videoURL;
        // this.$refs.videoRef.load();
      }

      this.index++;
    }
  }
};
</script>

<style scoped>
#mediaPlayer {
  position: absolute;
  height: 100%;
}
</style>
