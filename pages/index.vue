<template>
  <section class="container">
    <h1 class="title">
      <span class="subtitle">🔀</span>
      emojidna
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
