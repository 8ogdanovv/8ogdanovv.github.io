<template>
  <a
    href="https://bit.ly/2PDFcv"
    class="logo-link"
    title="My CV .pdf"
    :class="logoClass"
    :style="{ fontSize: size, lineHeight: size }"
  >
    <span class="logo-span logo">
      BOGDANO
    </span>
    <span class="logo-image logo" :style="{ width: size, height: size }">
      VV
    </span>
  </a>
</template>

<script setup>
const { size, logoClass } = defineProps(['size', 'logoClass'])
</script>

<style lang="scss">
.logo-link {
  justify-self: start;
  align-self: start;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  border: 2px dashed var(--color33);
  box-sizing: content-box;
  font-family: 'Victor Mono', monospace;
  letter-spacing: -0.21ch;
  padding: 0 0.33rem 0.25rem 0.1rem;
  background: var(--color-op);
  font-weight: 700;
  z-index: 1;

  .logo-span {
    padding-right: 0.18rem;
    background: var(--color-op);
  }

  &:hover {
    background: var(--color0);
    border-color: var(--bg33);

    .logo-span {
      background: var(--color0);
      color: var(--bg0);
    }
  }

  .logo-image {
    position: relative;
    z-index: -2;

    &:before, &:after {
      position: absolute;
      content: '';
      top: 0;
      left: 0.015em;
      width: 100%;
      height: 100%;
      padding-right: 0.15rem;
    }

    &:before {
      clip-path: polygon(
        0% 0%, 100% 0%, 100% 100%, 0% 100%
      );
      background: transparent;
      z-index: -2;
    }

    &:after {
      clip-path: polygon(
        1% 13%, 10% 13%, 27.5% 77%, 45% 13%, 55% 13%, 74% 77%, 91% 13%, 99% 13%, 99% 100%, 1% 100%
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
