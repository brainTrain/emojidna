<template>
  <section class="container">
    <h1 class="title">
      <span class="subtitle">🔀</span>
      emojidnaz
      <span class="subtitle">🔀</span>
    </h1>
    
    <div class="dna-wrapper">
      <div class="dna-inputs-wrapper">
        <input
          v-model="leftStrand"
          class="dna-input"
          aria-label="left emoji DNA strand input"
        >
        <input
          v-model="rightStrand"
          class="dna-input"
          aria-label="right emoji DNA strand input"
        >
      </div>
      <DNA
        :left="leftStrand"
        :right="rightStrand"
        @dna-rendered="handleRenderedDNA"
      />
      <button
        v-clipboard:copy="renderedDNA"
        v-clipboard:success="handleCopySuccess"
        v-clipboard:error="handleCopyError"
      >
        Copy DNA
      </button>
    </div>
  </section>
</template>

<script>
import Vue from 'vue';
import vueClipboard from 'vue-clipboard2';
import Noty from 'noty';

import DNA from '~/components/dna.vue'

import '~/assets/noty.css';
import '~/assets/noty-semanticui.css';

// TODO: research/decide if this should be in the global nuxt /plugins dir
Vue.use(vueClipboard);

const DEFAULT_LEFT_STRAND = '🧠';
const DEFAULT_RIGHT_STRAND = '🚂';
const NOTY_BASE_CONFIG = {
  theme: 'semanticui',
  timeout: 500,
  progressBar: false,
};

export default {
  components: {
    DNA,
  },
  data: function () {
    const {
      leftStrand,
      rightStrand,
    } = this.getStrandsFromUrl();

    return {
      leftStrand: leftStrand || DEFAULT_LEFT_STRAND,
      rightStrand: rightStrand || DEFAULT_RIGHT_STRAND,
      renderedDNA: '',
    }
  },
  watch: {
    '$route.query.leftStrand': function (leftStrand) {
      this.setStrands();
    },
    '$route.query.rightStrand': function (rightStrand) {
      this.setStrands();
    },
    leftStrand: {
      handler: function (newLeft) {
        this.setQueryParams();
      },
    },
    rightStrand: {
      handler: function (newRight) {
        this.setQueryParams();
      },
    },
  },
  created: function () {
    this.setQueryParams();
  },
  methods: {
    getStrandsFromUrl: function () {
      const {
        query: {
          leftStrand,
          rightStrand,
        } = {},
      } = this.$route;

      return {
        leftStrand,
        rightStrand,
      };
    },
    setStrands: function () {
      const {
        leftStrand,
        rightStrand,
      } = this.getStrandsFromUrl();

      this.leftStrand = leftStrand;
      this.rightStrand = rightStrand;
    },
    setQueryParams: function () {
      const {
        leftStrand,
        rightStrand,
      } = this;
      const query = {
        ...this.$route.query,
        leftStrand,
        rightStrand,
      };

      this.$router.push({ query });
    },
    handleRenderedDNA: function (renderedDNA) {
      this.renderedDNA = renderedDNA;
    },
    handleCopySuccess: function () {
      console.log('handleCopySuccess')
      new Noty({
        ...NOTY_BASE_CONFIG,
        text: 'Successfully copied Emoji DNA!!!1 \\o/',
        type: 'success',
      }).show();
    },
    handleCopyError: function () {
      new Noty({
        ...NOTY_BASE_CONFIG,
        text: 'Error copying Emoji DNA.. :\'(',
        type: 'error',
      }).show();
    },
  },
}
</script>

<style>

.container {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: space-evenly;
  align-items: center;
  text-align: center;
}

.dna-wrapper {
  height: 350px;
  width: 100px;
  display: inline-block;
}

.dna-inputs-wrapper {
  display: grid;
  grid-template-columns: 1fr 1fr;
  margin-bottom: 1rem;
}

.dna-input {
  border: none;
  border-bottom: 2px solid #CCC;
  width: 3rem;
  font-size: 2rem;
}

.title {
  font-family: 'Quicksand', 'Source Sans Pro', -apple-system, BlinkMacSystemFont,
    'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
  display: block;
  font-weight: 400;
  font-size: 3rem;
  color: #35495e;

}

.subtitle {
  transform: rotate(-90deg);
  font-size: 2rem;
  display: inline-block;
}
</style>
