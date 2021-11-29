<template>
  <div class="root">
    <div class="decoration">
      <svg class="wave">
        <use xlink:href="/images/lotus/deco-bg.svg#main" />
      </svg>
    </div>
    <v-container :class="{ fixed: isDesktop }">
      <div class="item">
        <u-animate-container>
          <v-row :class="[isMobile ? 'column-reverse' : 'row']">
            <v-col cols="12" md="6">
              <div class="illustration-left">
                <section class="parallax-wrap" v-if="loaded">
                  <parallax
                    :speed-factor="isMobile ? 0 : 0.15"
                    :section-height="isMobile ? 0 : 400"
                    direction="up"
                  >
                    <div class="viewport">
                      <figure class="figure screen">
                        <img :src="imgAPI.lotus[0]" alt="screen" />
                      </figure>
                    </div>
                  </parallax>
                </section>
                <section
                  class="parallax-wrap"
                  v-if="loaded && !isMobile"
                >
                  <parallax
                    :speed-factor="isMobile ? 0 : 0.15"
                    :section-height="100"
                    direction="down"
                  >
                    <div class="viewport">
                      <figure class="figure graphic">
                        <img :src="imgAPI.lotus[1]" alt="illustration" />
                      </figure>
                    </div>
                  </parallax>
                </section>
                <parallax-medium />
              </div>
            </v-col>
            <v-col md="6" cols="12">
              <u-animate
                :offset="-100"
                name="fadeInLeftShort"
                delay="0.5s"
                duration="0.5s"
              >
                <div class="desc">
                  <title-main :align="isMobile ? 'center' : 'left'">
                    <span>
                      {{ $t('lotusLanding.feature_title1') }}
                      <strong>
                        {{ $t('lotusLanding.feature_titlestrong1') }}
                      </strong>
                    </span>
                  </title-main>
                  <h6 class="use-text-subtitle2" :class="[isMobile ? 'text-center' : 'text-left']">
                    {{ $t('lotusLanding.feature_desc1') }}
                  </h6>
                  <v-btn color="primary" large class="btn">
                    {{ $t('lotusLanding.see_detail') }}
                  </v-btn>
                </div>
              </u-animate>
            </v-col>
          </v-row>
        </u-animate-container>
      </div>
      <div class="item">
        <v-row>
          <v-col md="6" cols="12">
            <u-animate-container>
              <u-animate
                :offset="10"
                name="fadeInRightShort"
                delay="0.5s"
                duration="0.5s"
              >
                <div class="desc">
                  <title-main :align="isMobile ? 'center' : 'right'">
                    <span>
                      {{ $t('lotusLanding.feature_title1') }}
                      <strong>
                        {{ $t('lotusLanding.feature_titlestrong2') }}
                      </strong>
                    </span>
                  </title-main>
                  <h6 class="use-text-subtitle2" :class="[isMobile ? 'text-center' : 'text-right']">
                    {{ $t('lotusLanding.feature_desc2') }}
                  </h6>
                  <div :class="[isMobile ? 'text-center' : 'text-right']">
                    <v-btn color="primary" large class="btn">
                      {{ $t('lotusLanding.see_detail') }}
                    </v-btn>
                  </div>
                </div>
              </u-animate>
            </u-animate-container>
          </v-col>
          <v-col md="6" cols="12">
            <div class="illustration-right">
              <section class="parallax-wrap" v-if="loaded">
                <parallax
                  :speed-factor="isMobile ? 0 : 0.15"
                  :section-height="isMobile ? 0 : 300"
                  direction="up"
                >
                  <div class="viewport">
                    <figure class="figure screen">
                      <img :src="imgAPI.lotus[2]" alt="screen" />
                    </figure>
                  </div>
                </parallax>
              </section>
              <section
                class="parallax-wrap"
                v-if="loaded && !isMobile"
              >
                <parallax
                  :speed-factor="isMobile ? 0 : 0.15"
                  :section-height="100"
                  direction="down"
                >
                  <div class="viewport">
                    <figure class="graphic">
                      <img :src="imgAPI.lotus[3]" alt="illustration" />
                    </figure>
                  </div>
                </parallax>
              </section>
              <parallax-medium />
            </div>
          </v-col>
        </v-row>
      </div>
    </v-container>
  </div>
</template>

<style lang="scss" scoped>
@import './feature-style.scss';
</style>

<script>
import Parallax from 'vue-parallaxy'
import imgAPI from '~/static/images/imgAPI'
import ParallaxMedium from '../Parallax/Medium'
import ParallaxLarge from '../Parallax/Large'
import Title from '../Title'

export default {
  components: {
    Parallax,
    ParallaxMedium,
    ParallaxLarge,
    'title-main': Title
  },
  data() {
    return {
      imgAPI: imgAPI,
      loaded: false
    }
  },
  mounted() {
    this.loaded = true
  },
  computed: {
    isDesktop() {
      const lgUp = this.$store.state.breakpoints.lgUp
      return lgUp.indexOf(this.$mq) > -1
    },
    isMobile() {
      const smDown = this.$store.state.breakpoints.smDown
      return smDown.indexOf(this.$mq) > -1
    }
  }
}
</script>
