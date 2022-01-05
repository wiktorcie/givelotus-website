<template>
  <div class="root">
    <div class="decoration">
      <svg class="left-deco">
        <use xlink:href="/images/lotus/deco-bg-left.svg#main" />
      </svg>
      <svg class="right-deco">
        <use xlink:href="/images/lotus/deco-bg-right.svg#main" />
      </svg>
    </div>
    <v-container :class="{ fixed: isDesktop }">
      <div class="container">
        <div class="item text-center pr-10">
          <h3 class="use-text-title">
            {{ $t('lotusLanding.banner_title') }}
            <strong>
              {{ $t('lotusLanding.banner_titlestrong') }}
            </strong>
          </h3>
          <p class="use-text-subtitle">
            {{ $t('lotusLanding.banner_subtitle') }}
          </p>

        </div>
        <div ref="videoContainer" class="item text-center">
          <video autoplay muted controls width="450">

              <source src="/videos/givelotus.mp4"
                      type="video/mp4">


              Sorry, your browser doesn't support embedded videos.
          </video>

          <!-- <vue-flv-player
            style="border-radius: 5%"
            controls
            autoplay
            :mediaDataSource="mediaDataSource"
            :width="width"
            :height="height"
            :muted="true"
            :source="src"
            type="mp4" /> -->
        </div>
      </div>
    </v-container>
    <div class="deco">
      <hidden point="mdDown">
        <div :class="{ hide: hide }" class="deco-inner">
          <div class="wave wave-one" />
          <div class="wave wave-two" />
        </div>
      </hidden>
      <div class="wave wave-cover" />
    </div>
  </div>
</template>

<style lang="scss" scoped>
@import './banner-style.scss';
</style>

<script>
import imgAPI from '~/static/images/imgAPI'
import Hidden from '../Hidden'

export default {
  components: {
    Hidden,
  },
  data() {
    return {
      src: "https://firebasestorage.googleapis.com/v0/b/cashcs-go.appspot.com/o/givelotus.mp4?alt=media&token=7aaf2bbc-8bab-441a-af29-db75db164697",
      hide: false,
      mediaDataSource: {
        url: "https://firebasestorage.googleapis.com/v0/b/cashcs-go.appspot.com/o/givelotus.mp4?alt=media&token=7aaf2bbc-8bab-441a-af29-db75db164697"
      },
      width: 416,
      height: 400,
      imgAPI: imgAPI,
      dialog: false,
    }
  },
  mounted () {
    this.$nextTick(() => {
      console.log(this.$refs.videoContainer.offsetWidth);
      window.addEventListener("resize", this.resizeVideo);
      this.resizeVideo();
    });
  },
  methods: {
    getWindowWidth() {
      this.windowWidth = document.documentElement.clientWidth
    },
    resizeVideo(){
      this.$nextTick();

      this.width = this.$refs.videoContainer.offsetWidth
      // this.height = this.$refs.videoContainer.offsetWidth
    }
  },
  computed: {
    isDesktop() {
      const lgUp = this.$store.state.breakpoints.lgUp
      return lgUp.indexOf(this.$mq) > -1
    }
  }
}
</script>
