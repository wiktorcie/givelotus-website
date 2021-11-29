<template>
  <div class="root">
    <v-container class="fixed-width">
      <v-row class="spacing6">
        <v-col md="6" class="pa-6">
          <title-main :align="isMobile ? 'center' : 'left'">
            <strong>
              FAQ
            </strong>
          </title-main>
          <p
            class="text use-text-subtitle2"
            :class="[isMobile ? 'text-center' : 'text-left']"
          >
            {{ $t('lotusLanding.faq_subtitle') }}
          </p>
          <hidden point="smDown">
            <div class="illustration">
              <parallax-medium />
              <img src="/images/lotus/faq.png" alt="illustration" />
            </div>
          </hidden>
        </v-col>
        <v-col md="6" cols="12" class="pa-6">
          <div class="accordion">
            <v-expansion-panels
              v-model="panel"
              active-class="expanded"
            >
              <v-expansion-panel
                v-for="(item, index) in faqData"
                :key="index"
                class="paper"
              >
                 <v-expansion-panel-header class="content">
                  <p class="heading">
                    {{ item.q }}
                  </p>
                </v-expansion-panel-header>
                <v-expansion-panel-content class="detail">
                  <p>
                    {{ item.a }}
                  </p>
                </v-expansion-panel-content>
              </v-expansion-panel>
            </v-expansion-panels>
          </div>
        </v-col>
      </v-row>
    </v-container>
  </div>
</template>

<style lang="scss" scoped>
@import 'faq-style.scss';
</style>

<script>
import Hidden from '../Hidden'
import ParallaxMedium from '../Parallax/Medium'
import Title from '../Title'

const faqData = [
  {
    q: 'How do I start mining?',
    a:
      'Vivamus sit amet interdum elit. Proin lacinia erat ac velit tempus auctor.'
  },
  {
    q: 'How do I get hold of Lotus?',
    a:
      'You can use this faucet ->>. Or you can get Lotus on our telegram group ->. '
  },
  {
    q: 'What are available wallets?',
    a:
      'Vivamus sit amet interdum elit. Proin lacinia erat ac velit tempus auctor. '
  },
  {
    q: 'How can I contribute to the project?',
    a:
      'Vivamus sit amet interdum elit. Proin lacinia erat ac velit tempus auctor. '
  },
  {
    q: 'Pellentesque ac bibendum tortor?',
    a:
      'Vivamus sit amet interdum elit. Proin lacinia erat ac velit tempus auctor. '
  }
]

export default {
  components: {
    Hidden,
    ParallaxMedium,
    'title-main': Title
  },
  data() {
    return {
      panel: 0,
      faqData: faqData
    }
  },
  computed: {
    isMobile() {
      const smDown = this.$store.state.breakpoints.smDown
      return smDown.indexOf(this.$mq) > -1
    }
  }
}
</script>
