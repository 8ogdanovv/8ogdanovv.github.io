<template>
  <a
    href="https://bit.ly/2PDFcv"
    class="logo-link"
    title="My CV .pdf"
    :class="logoClass"
    :style="{ fontSize: size, lineHeight: size }"
  >
    <span class="logo-span">
      BOGDANO
    </span>
    <span class="logo-image" :style="{ width: size, height: size }">
      VV
    </span>
  </a>
</template>

<script setup>
import { ref } from 'vue'
import getTheme from '@/helpers/getTheme'

const theme = ref(getTheme())
const { size, logoClass } = defineProps(['size', 'logoClass'])

</script>
<style lang="scss">
.logo-link {
  justify-self: start;
  align-self: start;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  border: 0.125rem dashed var(--color50);
  box-sizing: content-box;
  font-family: 'Victor Mono', monospace;
  letter-spacing: -0.24ch;
  padding-right: 0.072ch;
  background: var(--color-op);

  .logo-span {
    padding-right: 0.05em;
    background: var(--color-op);
  }

  &:hover {
    background: var(--color0);
    border: 0.125rem dashed var(--bg50);

    .logo-span {
      background: var(--color0);
      color: var(--bg0);
    }
  }

  .logo-image {
    position: relative;
    padding-right: 0.75em;
    z-index: 2;

    &:before, &:after {
      position: absolute;
      content: '';
      top: 0;
      left: 0.015em;
      width: 100%;
      height: 100%;
      padding-right: 0.018em;
    }

    &:before {
      clip-path: polygon(
        0% 0%, 100% 0%, 100% 100%, 0% 100%
      );
      background: var(--bg0);
      z-index: -2;
    }

    &:after {
      clip-path: polygon(
        1% 11%, 10% 11%, 27.5% 73%, 45% 11%, 55% 11%, 72.5% 73%, 90% 11%, 100% 11%, 100% 100%, 1% 100%
      );
      background: var(--accent0);
      z-index: -1;
    }

  }
  &:hover .logo-image {
    color: var(--bg0);
  }

  &:hover .logo-image:before {
    background: var(--color0);
  }

  &:hover .logo-image:after {
    background: var(--accent1);
  }
}
</style>
