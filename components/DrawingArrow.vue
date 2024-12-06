<template>
  <svg
    width="183px"
    height="199px"
    viewBox="0 0 183 199"
    xmlns="http://www.w3.org/2000/svg"
    xmlns:xlink="http://www.w3.org/1999/xlink"
    xmlns:sketch="http://www.bohemiancoding.com/sketch/ns"
  >
    <title>intro_anim_arrow</title>
    <g id="Page-1" stroke="none" stroke-width="1" fill="none" fill-rule="evenodd">
      <g id="intro_anim_arrow" stroke="#FFFFFF">
        <g id="solid-line">
          <path
            d="M0.8984375,0.740234375 C0.8984375,0.740234375 97.5703125,1.46484375 112.949219,98.4277344 C128.328125,195.390625 179.106445,191.580078 179.106445,191.580078"
            class="line"
          ></path>
        </g>
        <g id="dashed-line">
          <path
            d="M0.8984375,0.740234375 C0.8984375,0.740234375 97.5703125,1.46484375 112.949219,98.4277344 C128.328125,195.390625 179.106445,191.580078 179.106445,191.580078"
            class="dashed"
            stroke="white"
            stroke-width="1"
          ></path>
        </g>
        <g
          id="arrow"
          class="arrow"
          transform="translate(179.444997, 192.049525) rotate(6.000000) translate(-179.444997, -192.049525) translate(176.944997, 187.049525)"
          stroke-linecap="square"
        >
          <path
            d="M4.5,0.5 L0.286957741,4.71304226"
            id="top-arrow"
            class="top-arrow"
            transform="translate(2.500000, 2.500000) scale(1, -1) translate(-2.500000, -2.500000)"
          ></path>
          <path
            d="M4.53856898,4.73593979 L0.570944003,9.1749871"
            id="bottom-arrow"
            class="bottom-arrow"
            transform="translate(2.554756, 6.955463) scale(-1, -1) translate(-2.554756, -6.955463)"
          ></path>
        </g>
      </g>
    </g>
  </svg>
</template>

<style scoped>
.dashed {
  stroke-dasharray: 3;
  stroke-width: 1;
}

.line {
  stroke-dasharray: 1000;
  stroke-dashoffset: 1000;
  animation: dash 5000ms linear forwards infinite;
}

.arrow {
  opacity: 0;
  animation: show 200ms forwards;
  animation-delay: 1550ms;
  animation-iteration-count: 1;
  animation-fill-mode: forwards;
  pointer-events: none;
}

@keyframes show {
  0% {
    opacity: 0;
  }
  100% {
    opacity: 1;
  }
}

@keyframes dash {
  from {
    stroke-dashoffset: 1000;
  }
  to {
    stroke-dashoffset: 0;
  }
}
</style>
