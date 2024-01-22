<template>
  <a
    href="https://bit.ly/2pdfCV"
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
  font-family: 'Impact', sans-serif;
  letter-spacing: -0.15ch;

  .logo-span {
    background: var(--color-op);
    padding-right: 0.05em;
  }

  &:hover .logo-span {
    filter: invert(1);
  }

  .logo-image {
    position: relative;
    margin-right: -0.025em;
    z-index: 2;

    &:before, &:after {
      position: absolute;
      content: '';
      top: 0;
      left: -0.019em;
      width: 100%;
      height: 100%;
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
        0% 10%, 23.5% 10%, 28% 65%, 33% 10%, 67.5% 10%, 72.5% 65%, 77% 10%, 100% 10%, 100% 100%, 0% 100%
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
