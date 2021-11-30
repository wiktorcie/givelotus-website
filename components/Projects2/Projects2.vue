<template>
  <div class="root">
    <v-container class="fixed-width">

      <div class="carousel-handle">
        <div v-if="loaded" class="carousel-wrap">
          <slick
            ref="slick"
            :options="slickOptions"
          >
            <div class="item">
              <div class="carousel-prop">
                <div />
              </div>
            </div>
            <div
              v-for="(item, index) in projectsList"
              :key="index"
              class="item"
            >
              <card
                :title="item.title"
                :desc="item.desc"
                :img="item.img"
                :url="item.url"
                :button="$t('lotusLanding.services_button')"
              />
            </div>
            <div class="item">
              <div class="carousel-prop">
                <div />
              </div>
            </div>
          </slick>
        </div>
      </div>

      <!-- <div class="floating-title">
        <v-container class="fixed-width">
          <div class="title">
            <title-icon
              :text="$t('lotusLanding.services_title')"
              icon=""
              extended
            />
            <nav class="arrow">
              <v-btn
                fab
                small
                aria-label="next"
                class="margin"
                @click="next()"
              >
                <v-icon>mdi-arrow-left</v-icon>
              </v-btn>
              <v-btn
                fab
                small
                aria-label="prev"
                class="margin"
                @click="prev()"
              >
                <v-icon>mdi-arrow-right</v-icon>
              </v-btn>
            </nav>

          </div>
        </v-container>
      </div> -->
  </v-container>
  </div>
</template>

<style lang="scss" scoped>
@import './projects2-style.scss';
</style>

<script>
import imgApi from '~/static/images/imgAPI'
import Card from '../Cards/Default'
import TitleIcon from '../Title/WithIcon'

export default {
  components: {
    Card,
    TitleIcon,
    Slick: () => import('vue-slick')
  },
  data() {
    return {
      loaded: false,
      slickOptions: {
        dots: false,
        infinite: false,
        centerMode: false,
        speed: 350,
        slidesToShow: 4,
        autoplay: true,
        autoplaySpeed: 2000,
        arrows: false,
        slidesToScroll: 1,
        variableWidth: true,
        responsive: [
          {
            breakpoint: 1100,
            settings: {
              slidesToShow: 4
            }
          },
          {
            breakpoint: 800,
            settings: {
              slidesToShow: 2
            }
          }
        ]
      },
      projectsList: [
        {
          title: 'Logos Foundation',
          desc: this.$t('lotusLanding.logos_desc'),
          url: 'https://github.com/LogosFoundation',
          img: imgApi.projects[3]
        },
        {
          title: '',
          desc: this.$t('lotusLanding.stampchat_desc'),
          url: 'https://stampchat.io/',
          img: imgApi.projects[0]
        },
        {
          title: '',
          desc: this.$t('lotusLanding.becash_desc'),
          url: 'https://be.cash/',
          img: imgApi.projects[1]
        },
        {
          title: '',
          desc: this.$t('lotusLanding.bitcoin_abc_desc'),
          url: 'https://bitcoinabc.org/',

          img: imgApi.projects[2]
        }
      ]
    }
  },
  mounted() {
    this.loaded = true
    const props = window.innerWidth > 1400 ? 1 : 2 // div.carousel-props length for screen < 1400px and (-1) for screen > 1400px
    const lastSlide = Math.floor(this.projectsList.length + props - this.slickOptions.slidesToShow)
    setTimeout(() => {
      if (window.innerWidth > 1200 && !this.$vuetify.rtl) {
        this.$refs.slick.goTo(lastSlide)
      }
    }, 100)
  },
  methods: {
    next: function() {
      this.$refs.slick.next()
    },
    prev: function() {
      this.$refs.slick.prev()
    }
  }
}
</script>
