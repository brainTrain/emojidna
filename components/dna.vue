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
const dnaTemplateTwitter =
`x　  o
   xo
　 o
  ox
 o　 x
o　　x
o　　x
 o　x
   ox
    x
  x o
 x　  o
x　　  o
x　　 o
 x　 o
  xo
     o
  o   x
`;
const dnaTemplate = `
 x　 o
  x o
　 o
　o x
 o　 x
o　　 x
o　　 x
 o　 x
  o x
　 x
　x o
 x　 o
x　　 o
x　　 o
 x　 o
　x o
   o
  o  x
`;

export default {
  name: 'DNA',
  props: {
    left: {
      type: String,
      default: 'x',
    },
    right: {
      type: String,
      default: 'o',
    },
  },
  data: function () {
    return {
      renderedDNA: '',
    }
  },
  watch: {
    left: {
      immediate: true,
      handler: function (newLeft) {
        this.drawDNA(newLeft, this.right);
      },
    },
    right: {
      immediate: true,
      handler: function (newRight) {
        this.drawDNA(this.left, newRight);
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
