<template>
  <div class="root">
    <v-container class="fixed-width">
      <!--
      <nav class="">
        <v-btn
          small
          tile
          aria-label="next"
          class="margin carousel-arrow-left"
          @click="prev()"
        >
          <v-icon>mdi-arrow-left</v-icon>
        </v-btn>
        <v-btn
          small
          tile
          aria-label="prev"
          class="margin carousel-arrow-right"
          @click="next()"
        >
          <v-icon>mdi-arrow-right</v-icon>
        </v-btn>
      </nav>
       -->

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

          </slick>

        </div>
      </div>
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
        arrows: false,

        variableWidth: true,
        infinite: true,

        centerMode: true,

        speed: 500,
        slidesToShow: 4,
        autoplay: true,
        autoplaySpeed: 3500,
        slidesToScroll: 1,
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
        },


        // This is a terrible hack that I hate but i need to move on
        // the problem is:
        // There is a white space in a carousel at viewports over >1280px
        // It doesn't happen under that.
        // This might be a bug with slick carousel
        // https://github.com/akiran/react-slick/issues/540
        // I don't know how to fix it and need to move on with other.
        // This is my attempt at hiding the white space by adding more
        // items so user won't see the white space.
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
        },
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
    setTimeout(() => {
      if (window.innerWidth > 1200 && !this.$vuetify.rtl) {
        this.$refs.slick.goTo(2)
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