<template>
  <textarea
    v-model="renderedDNA"
    class="dna-container"
    aria-label="rendered emoji DNA textarea"
  />
</template>

<script>
const LEFT_CONST = 'x';
const RIGHT_CONST = 'o';
const IDEAL_SPACE_CONST = '　';

const dnaTemplateTwitter =
`${LEFT_CONST}　${RIGHT_CONST}
   ${LEFT_CONST}${RIGHT_CONST}
　 ${RIGHT_CONST}
　${RIGHT_CONST}${LEFT_CONST}
 ${RIGHT_CONST}　${LEFT_CONST}
${RIGHT_CONST}　　${LEFT_CONST}
${RIGHT_CONST}　　${LEFT_CONST}
 ${RIGHT_CONST}　${LEFT_CONST}
   ${RIGHT_CONST}${LEFT_CONST}
　  ${LEFT_CONST}
　${LEFT_CONST} ${RIGHT_CONST}
 ${LEFT_CONST}　 ${RIGHT_CONST}
${LEFT_CONST}　　${RIGHT_CONST}
${LEFT_CONST}　　 ${RIGHT_CONST}
 ${LEFT_CONST}　  ${RIGHT_CONST}
　${LEFT_CONST}${RIGHT_CONST}
     ${RIGHT_CONST}
  ${RIGHT_CONST}    ${LEFT_CONST}`;

export default {
  name: 'DNA',
  props: {
    left: {
      type: String,
      default: '',
    },
    right: {
      type: String,
      default: '',
    },
    handleGetRenderedDNA: {
      type: Function,
      default: () => console.warn('handleGetRenderedDNA() is not implemented'),
    },
  },
  data: function () {
    return {
      renderedDNA: '',
    };
  },
  watch: {
    left: {
      immediate: true,
      handler: function (newLeft) {
        this.drawDNA(newLeft, this.right);
        this.getRenderedDNA();
      },
    },
    right: {
      immediate: true,
      handler: function (newRight) {
        this.drawDNA(this.left, newRight);
        this.getRenderedDNA();
      },
    },
  },
  methods: {
    drawDNA: function (left, right) {
      const dnaCharacterMap = {
        [LEFT_CONST]: left,
        [RIGHT_CONST]: right,
      };

      const dnaMatchRegex = new RegExp(`${LEFT_CONST}|${RIGHT_CONST}`,'gi');
      const newDNATemplate = dnaTemplateTwitter.replace(dnaMatchRegex, function (matchedString) {
        return dnaCharacterMap[matchedString] || '';
      });

      this.renderedDNA = newDNATemplate;
    },
    getRenderedDNA: function () {
      this.$emit('dna-rendered', this.renderedDNA);
    },
  },
}
</script>

<style>
.dna-container {
  /*animation: turn 5s infinite;*/
  height: 100%;
  width: 100%;
  border: none;
  text-align: center;
}

@keyframes turn {
  0 {
    transform: rotateY(0deg);
  }
  50% {
    transform: rotateY(180deg);
  }
  100% {
    transform: rotateY(0deg);
  }
}
</style>
