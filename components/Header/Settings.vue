<template>
  <v-menu
    v-model="open"
    :close-on-content-click="closeOnContentClick"
    transition="slide-y-transition"
    offset-y
    nudge-top="-6"
    bottom
    class="menu-setting"
  >
    <template v-slot:activator="{ on }">
      <div class="setting">
        <v-btn
          fab
          text
          small
          v-on="on"
          class="ma-3"
        >
          <v-icon
            :class="{ invert: invert, active: open }"
            class="icon"
          >
            settings
          </v-icon>
        </v-btn>
      </div>
    </template>
    <div class="popover ocean-blue-var">
      <v-list class="mode-menu">
        <v-subheader>{{ $t('agencyLanding.header_theme') }}</v-subheader>
        <v-list-item>
          <v-list-item-content>
            <div class="flex-menu">
              <label>
                {{ $t('agencyLanding.header_light') }}
              </label>
              <v-switch
                v-model="dark"
                label=""
                class="switch-toggle"
                color="primary"
                @change="setDark()"
              />
              <label>
                {{ $t('agencyLanding.header_dark') }}
              </label>
            </div>
          </v-list-item-content>
        </v-list-item>
      </v-list>
      <v-divider />
      <v-list class="lang-menu">      
      
        <v-list-item>
          <v-list-item-avatar>
            <v-img src="https://cdn.vuetifyjs.com/images/john.png"></v-img>
          </v-list-item-avatar>
        </v-list-item>

        <v-list-item link>
          <v-list-item-content>
            <v-list-item-title class="text-h6">
              John Leider
            </v-list-item-title>
            <v-list-item-subtitle>john@vuetifyjs.com</v-list-item-subtitle>
          </v-list-item-content>

          <v-list-item-action>
            <v-icon>mdi-menu-down</v-icon>
          </v-list-item-action>
        </v-list-item>
  <v-list-item>
             <v-btn :href="link.agency.login" class="button primary">
              Login
          </v-btn>
        </v-list-item>
      
        <!-- <v-list-item
          v-for="locale in $i18n.locales"
          :key="locale.code"
          class="lang-list"
          @click="switchLang(locale.code)"
        >
          <v-list-item-avatar class="flag">
            <i :class="locale.code" />
          </v-list-item-avatar>
          <v-list-item-content>
            <v-list-item-title class="lang-opt">
              {{ $t('common.'+locale.code) }}
            </v-list-item-title>
          </v-list-item-content>
          <v-list-item-action>
            <v-icon
              v-if="locale.code === $i18n.locale"
              color="primary"
            >
              mdi-check
            </v-icon>
          </v-list-item-action>
        </v-list-item> -->

      </v-list>

    </div>
  </v-menu>
</template>

<style lang="scss" scoped>
@import './header-style.scss';
</style>

<script>

import link from '~/static/text/link'
import { mapGetters, mapState } from 'vuex'

let darkMode = false
if (typeof Storage !== 'undefined') { // eslint-disable-line
  darkMode = localStorage.getItem('luxiDarkMode') || false
}

export default {
  props: {
    invert: {
      type: Boolean,
      default: false
    }
  },
  data: () => ({
      link: link,
    dark: darkMode === 'true',
    rtl: false,
    open: false,
    closeOnContentClick: false
  }),
  computed: {
    ...mapState(['counter', 'darkMode']),
    ...mapGetters(['getDir'])
  },
  methods: {
    switchLang: function(val) {
      this.$i18n.setLocale(val)
    },
    setDark: function() {
      localStorage.setItem('luxiDarkMode', this.dark)
      this.$vuetify.theme.dark = this.dark
    },
    setDirection: function() {
      this.$vuetify.rtl = this.rtl
      document.dir = this.rtl ? 'rtl' : 'ltr'
    }
  }
}
</script>
