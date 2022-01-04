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
      <div class="slider-wrap">
        <div class="text">
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
        <div>
          <vue-flv-player
            style="border-radius: 5%"
            controls
            autoplay
            width="670px"
            height="400px"
            :muted="true"
            :source="src"
            type="mp4" />
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
import youtube from '~/youtube'
import imgAPI from '~/static/images/imgAPI'
import link from '~/static/text/link'
import Hidden from '../Hidden'

export default {
  components: {
    Hidden,
  },
  data() {
    return {
      src: "/videos/givelotus.mp4",
      videoId: 'ujCfPhGrQ5A',
      hide: false,
      link: link,
      imgAPI: imgAPI,
      dialog: false,
      player: null,
      playerVars: {
        autoplay: 0,
        controls: 1,
        rel: 0,
        showinfo: 1,
        mute: 0,
        origin: 'https://localhost:8008'
      },
      yt: youtube
    }
  },
  methods: {
    handleVideoOpen() {
      if (!this.yt.use) {
        return false
      }
      this.dialog = true
      setTimeout(() => {
        this.player = this.$refs.youtube.player
        this.player.playVideo()
      }, 100)
    },
    handleVideoClose() {
      this.dialog = false
      this.player.pauseVideo()
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
