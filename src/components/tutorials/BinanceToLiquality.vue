<template>
  <div class="tutorials tutorial-background">
    <v-container class="tutorial-container">
      <div class="d-flex align-center">
        <router-link :to="{ name: 'Tutorials' }" class="mr-3">
          <v-img height="28" src="@/assets/tutorials/left-arrow.svg" alt="Left arrow" contain/>
        </router-link>
        <h1>{{ $t('tutorials.binance.title') }}</h1>
        <img class="mx-2" src="@/assets/wallets/binance.svg" alt="Binance Logo" />
      </div>

      <v-row class="tutorial-steps" v-for="elements in this.groupedElements" :key="elements.id">
        <v-col
          v-for="element in elements"
          :key="element.id"
          cols="12"
          :md="element.number === 4 ? 8 : 4"
        >
          <div class="d-flex align-center tutorial-step-title justify-sm-center justify-md-start">
            <div class="tutorial-step-number flex-shrink-0 d-flex align-center justify-center">
              <h2>{{ element.number }}.</h2>
            </div>
            <div class="d-flex align-center">
              <h2 class="tutorial-step-description">{{ element.title }}</h2>
            </div>
          </div>

          <v-img :src="element.image" alt="Tutorial step" class="mx-auto tutorial-step-image" />
        </v-col>
      </v-row>
    </v-container>
    <div class="frog-container" style="position: relative">
      <img src="@/assets/tutorials/frog.svg" alt="" class="tutorial-frog" />
    </div>
  </div>
</template>

<script>
import Step01 from '@/assets/tutorials/binance-to-liquality/step01.png';
import Step02 from '@/assets/tutorials/binance-to-liquality/step02.png';
import Step03 from '@/assets/tutorials/binance-to-liquality/step03.png';
import Step04 from '@/assets/tutorials/binance-to-liquality/step04.png';
import Step05 from '@/assets/tutorials/binance-to-liquality/step05.png';
import Step06 from '@/assets/tutorials/binance-to-liquality/step06.png';
import Step07 from '@/assets/tutorials/binance-to-liquality/step07.png';

export default {
  data() {
    return {
      steps: [
        {
          number: 1,
          title: this.$t('tutorials.binance.subtitle1'),
          image: Step01,
        },
        {
          number: 2,
          title: this.$t('tutorials.binance.subtitle2'),
          image: Step02,
        },
        {
          number: 3,
          title: this.$t('tutorials.binance.subtitle3'),
          image: Step03,
        },
        {
          number: 4,
          title: this.$t('tutorials.binance.subtitle4'),
          image: Step04,
        },
        {
          number: 5,
          title: this.$t('tutorials.binance.subtitle5'),
          image: Step05,
        },
        {
          number: 6,
          title: this.$t('tutorials.binance.subtitle6'),
          image: Step06,
        },
        {
          number: 7,
          title: this.$t('tutorials.binance.subtitle7'),
          image: Step07,
        },
      ],
    };
  },
  computed: {
    groupedElements() {
      return [
        [this.steps[0], this.steps[1], this.steps[2]],
        [this.steps[3], this.steps[4]],
        [this.steps[5], this.steps[6]],
      ];
    },
  },
};
</script>
<style scoped>
.tutorial-step-number {
  background-color: #ff9153;
}

.tutorial-step-description {
  line-height: 28px;
}

@media screen and (max-width: 1365px) {
  .tutorial-step-title {
    height: 224px;
  }
}
@media screen and (min-width: 1366px) {
  .tutorial-step-title {
    height: 122px;
  }
}
</style>
