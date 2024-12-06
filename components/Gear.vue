<template>
  <div class="parent">
    <div class="gear" :style="gearStyle">
      <div class="center"></div>
      <div
        class="tooth"
        v-for="n in toothCount"
        :key="n"
        :style="getToothStyle(n)"
      ></div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Gear',
  props: {
    /**
     * The base size of the gear in pixels.
     * All other dimensions scale proportionally based on this value.
     */
    size: {
      type: Number,
      default: 100,
      validator: value => value > 0,
    },
    /**
     * The rotation direction of the gear.
     * Accepts 'clockwise' or 'counterclockwise'.
     */
    direction: {
      type: String,
      default: 'clockwise',
      validator: value => ['clockwise', 'counterclockwise'].includes(value),
    },
    /**
     * Number of teeth on the gear.
     * Default is 4 to match the original setup.
     */
    toothCount: {
      type: Number,
      default: 4,
      validator: value => value > 0,
    },
  },
  computed: {
    /**
     * Computes the CSS variables based on the size prop.
     * These variables ensure all elements scale proportionally.
     */
    cssVars() {
      return {
        '--gear-size': `${this.size}px`,
        '--gear-center-size': `${this.size * 0.5}px`, // 50% of gear size
        '--gear-tooth-width': `${this.size * 0.225}px`, // 22.5% of gear size
        '--gear-tooth-height': `${this.size * 1.25}px`, // 125% of gear size
        '--gear-tooth-top': `${-this.size * 0.125}px`, // -12.5% of gear size
        '--gear-tooth-left': `${this.size * 0.375}px`, // 37.5% of gear size
        '--animation-direction':
          this.direction === 'clockwise' ? 'normal' : 'reverse',
      };
    },
    /**
     * Combines the CSS variables with the animation direction.
     */
    gearStyle() {
      return {
        ...this.cssVars,
      };
    },
  },
  methods: {
    /**
     * Calculates the rotation angle for each tooth based on its index.
     * Ensures even distribution of teeth around the gear.
     * @param {Number} index - The index of the tooth (1-based).
     * @returns {Object} - Inline style for the tooth.
     */
    getToothStyle(index) {
      const angle = (360 / this.toothCount) * (index - 1);
      return {
        transform: `rotate(${angle}deg)`,
      };
    },
  },
};
</script>

<style scoped>
.parent {
  display: flex;
  justify-content: center;
  align-items: center;
  height: calc(var(--gear-size) * 2.5); /* 2.5 times the gear size */
}

.gear {
  position: relative;
  width: var(--gear-size);
  height: var(--gear-size);
  background: #fff;
  border-radius: 50%;
  animation: spin 4s linear infinite;
  animation-direction: var(--animation-direction);
}

.center {
  position: absolute;
  top: calc((var(--gear-size) - var(--gear-center-size)) / 2);
  left: calc((var(--gear-size) - var(--gear-center-size)) / 2);
  width: var(--gear-center-size);
  height: var(--gear-center-size);
  background: #000;
  border-radius: 50%;
  z-index: 10;
}

.tooth {
  position: absolute;
  top: var(--gear-tooth-top);
  left: var(--gear-tooth-left);
  width: var(--gear-tooth-width);
  height: var(--gear-tooth-height);
  background: #fff;
  border-radius: 4px;
  z-index: 5;
}

@keyframes spin {
  from {
    transform: rotate(0deg);
  }
  to {
    transform: rotate(360deg);
  }
}
</style>
