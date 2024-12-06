<template>
  <div class="horizontal timeline">
    <div class="steps">
      <div
        v-for="({ step, description }, index) in steps"
        :key="index"
        :class="['step', { current: index === currentStep }]"
      >
        <span class="step-title">{{ step }}</span>
        <span class="description">{{ description }}</span>
      </div>
    </div>
    <div class="line" :style="{ width: lineWidth }"></div>
  </div>
</template>

<script setup>
import { ref, computed, watch } from 'vue'

const steps = [
  { 
    step: "LEXICAL ANALYSIS", 
    description: `
  { type: 'keyword', value: 'let' },
  { type: 'identifier', value: 'x' },
  { type: 'operator', value: '=' },
  { type: 'number', value: '42' },
  { type: 'punctuation', value: ';' }
  ` 
  },
  {
    step: "SYNTACTIC ANALYSIS", 
    description: `
    Converts tokens into AST
    Validates syntax
    Creates tree structure
    ` 
  },
  {
    step: "GENERATE AST", 
    description: `
    { 
        "type":"BinaryExpression",
        "left":{
            "type":"Literal",
            "value":2,
            "raw":"2"
        },
    }
    `
  }
]

const currentStep = ref(0)

const lineWidth = computed(() => {
  return `${(currentStep.value / (steps.length - 1)) * 100}%`
})

// Export for parent component to control
defineExpose({
  nextStep: () => {
    if (currentStep.value < steps.length - 1) {
      currentStep.value++
    }
  }
})
</script>

<style scoped>
.horizontal.timeline {
  display: flex;
  position: relative;
  flex-direction: row;
  justify-content: space-between;
  align-items: center;
  width: 80%;
}

.horizontal.timeline:before {
  content: "";
  display: block;
  position: absolute;
  width: 100%;
  height: 0.2em;
  background-color: #f0f0f0;
}

.line {
  display: block;
  position: absolute;
  height: 0.2em;
  background-color: #D2282C;
  transition: width 0.5s ease-in-out;
}

.steps {
  display: flex;
  position: relative;
  flex-direction: row;
  justify-content: space-between;
  align-items: center;
  width: 100%;
}

.step {
  display: block;
  position: relative;
  bottom: calc(100% + 1em);
  padding: 0.33em;
  margin: 0 2em;
  box-sizing: content-box;
  color: #D2282C;
  background-color: currentColor;
  border: 0.25em solid white;
  border-radius: 50%;
  z-index: 500;
  cursor: pointer;
}

.step:first-child {
  margin-left: 0;
}

.step:last-child {
  margin-right: 0;
  color: #D2282C;
}

.step span {
  position: absolute;
  top: calc(100% + 1em);
  left: 50%;
  transform: translateX(-50%);
  white-space: nowrap;
  color: #fff;
  opacity: 0.2;
  transition: opacity 0.8s ease-in-out;
}

.step.current span {
  opacity: 0.8;
  transition: opacity 0.8s ease-in-out;
}

.step.current:before {
  content: "";
  display: block;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  padding: 1em;
  background-color: currentColor;
  border-radius: 50%;
  opacity: 0;
  z-index: -1;
  animation-name: animation-timeline-current;
  animation-duration: 2s;
  animation-iteration-count: infinite;
  animation-timing-function: ease-out;
}

@keyframes animation-timeline-current {
  from {
    transform: translate(-50%, -50%) scale(0);
    opacity: 1;
  }
  to {
    transform: translate(-50%, -50%) scale(1);
    opacity: 0;
  }
}


.step span.description {
  margin-top: 10px;
  width: 260px;
  white-space: pre-wrap;
  line-height: 1.4;
}
</style>