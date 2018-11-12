<template>
  <section class="container">
    <h1 class="title">
      emojidna
    </h1>
    <h2 class="subtitle">🔀</h2>
    <div class="dna-inputs-wrapper">
      <input
        v-model="leftStrand"
        class="dna-input"
      >
      <input
        v-model="rightStrand"
        class="dna-input"
      >
    </div>
    {{ leftStrand }} {{ rightStrand }}
    <div class="dna-wrapper">
      <DNA
        :left="leftStrand"
        :right="rightStrand"
      />
    </div>
  </section>
</template>

<script>
import DNA from '~/components/dna.vue'

export default {
  components: {
    DNA
  },
  data: function () {
    return {
      leftStrand: '🧠',
      rightStrand: '🚂',
    }
  },
}
</script>

<style>

.container {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.dna-wrapper {
  height: 350px;
  width: 70px;
  display: inline-block;
}

.title {
  font-family: 'Quicksand', 'Source Sans Pro', -apple-system, BlinkMacSystemFont,
    'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;

}

.subtitle {
  transform: rotate(-90deg);
  display: inline;
}
</style>
