<template>
  <v-app class="app">
    <navbar :marketAddresses="markets" />
    <left-bar />
    <router-view />
    <v-dialog v-model="btcToRbtcDialog" width="350"
              overlay-opacity="0.8" overlay-color="#000">
      <v-card class="modal-convert-btn container" color="#013E2F">
        <v-row class="mx-0 pt-5 mb-3 d-flex justify-center">
          <h1 class="text-center">
            {{ $t('app.popup.title1') }}
          </h1>
        </v-row>
        <v-row class="mx-0 my-5 d-flex justify-center">
          <p class="text-center ma-0">
             {{ $t('app.popup.description1') }}
          </p>
        </v-row>
        <v-row class="mx-0 mt-8 mb-6 d-flex justify-center">
          <v-img height="60" alt="BTN icon" contain
                 src="@/assets/tutorials/btc-to-rbtc/BtcToRbtc.svg"/>
        </v-row>
        <v-row class="ma-0">
          <v-col class="d-flex justify-center">
            <v-btn @click="btcToRbtcDialog = false" width="95%"
                   outlined color="#fff">
              {{ $t('app.popup.button1') }}
            </v-btn>
          </v-col>
          <v-col class="d-flex justify-center">
            <v-btn @click="closeAndRedirect"
                   width="95%" color="#4CB163">
              {{ $t('app.popup.button2') }}
            </v-btn>
          </v-col>
        </v-row>
        <v-row class="ma-0 d-flex justify-center">
          <v-checkbox hide-details dark v-model="dontShowWelcomeModal"
            :label="$t('app.popup.description2')" class="mt-0" />
        </v-row>
      </v-card>
    </v-dialog>
  </v-app>
</template>

<script>
import { mapState } from 'vuex';
import Navbar from '@/components/menu/Navbar.vue';
import LeftBar from '@/components/menu/LeftBar.vue';
import { Comptroller } from '@/middleware';

export default {
  name: 'App',
  data() {
    return {
      btcToRbtcDialog: true,
      comptroller: null,
      markets: [],
      dontShowWelcomeModal: false,
    };
  },
  computed: {
    ...mapState({
      chainId: (state) => state.Session.chainId,
    }),
  },
  methods: {
    closeAndRedirect() {
      this.$router.push({ name: 'BtcToRbtc' });
      this.btcToRbtcDialog = false;
    },
    async loadMarkets() {
      this.markets = await this.comptroller.allMarkets;
    },
  },
  watch: {
    chainId(val) {
      if (val) {
        this.$forceUpdate();
      }
    },
    dontShowWelcomeModal() {
      localStorage.flag = !this.dontShowWelcomeModal;
    },
  },
  created() {
    this.comptroller = new Comptroller(this.chainId);
    this.loadMarkets();
  },
  mounted() {
    if (localStorage.flag) {
      this.btcToRbtcDialog = localStorage.flag === 'true';
    }
  },
  components: {
    Navbar,
    LeftBar,
  },
};
</script>
