<template>
  <button
    @click="toggleTheme"
    class="theme-toggler"
    :title="`Toggle theme to ${theme === 'light' ? 'dark' : 'light'}`"
  >
    <span
      id="spot"
      :style="{
        background: `radial-gradient(ellipse at ${offsetX}% ${offsetY}%, var(--accent1), var(--color0))`,
        fontSize: theme === 'light' ? '1.5rem' : '1.75rem',
      }"
    >
      {{ theme === 'light' ? '🌙' : '🌞' }}
    </span>

    <h2 v-show="false">
      {{ width }} {{ height }}<br />
      {{ x }} {{ y }}<br />
      {{ offsetX }} {{ offsetY }}
    </h2>
  </button>
</template>

<script setup>
import { ref, onMounted, watch, onUpdated } from 'vue'
import { useMouse, useWindowSize } from '@vueuse/core'
import getTheme from '@/helpers/getTheme'

const { x, y } = useMouse()
const { width, height } = useWindowSize()
const offsetX = ref(50)
const offsetY = ref(50)

const theme = ref(getTheme())

const toggleTheme = () => {
  theme.value = theme.value === 'light' ? 'dark' : 'light'
}

const setTheme = theme => {
  sessionStorage.setItem('theme', theme)
  document.documentElement.setAttribute('data-theme', theme)
  document.getElementById('favicon').href = theme === 'dark' ? '/favicon_dark.ico' : '/favicon_light.ico'
}

onMounted(() => setTheme(theme.value))

onUpdated(() => {
  offsetX.value = (x.value / width.value) * 100 || 50
  offsetY.value = (y.value / height.value) * 100 || 50
})

watch(theme, newTheme => setTheme(newTheme))
</script>

<style lang="scss">
[data-theme='dark'] {
  --theme-logo: './logo_dark.png';
  --theme-logo-inv: './logo_light.png';
  --is-dark: 1;
  --is-white: 0;
  --bg0: #131313;
  --bg50: #13131388;
  --bg2: #1a1a1a;

  --color-op: #000000;
  --color0: #ffffff;
  --color50: #ffffff88;

  --color1: #f4f7fa;
  --color2: #a8a8a8;
  --color3: #949494;

  --accent0: #0066cc;
  --accent50: #0066cc88;
  --accent1: #ffcc00;
  --accent2: hsl(210, 100%, 71%);

  --scrollbar-thumb: rgb(54, 54, 54);
  --scrollbar-track: rgb(90, 90, 90);

  --scrollbar-thumb_hover: rgb(21, 21, 21);
  --scrollbar-track_hover: rgb(106, 106, 106);

  --loader-bg-blend-mode: multiply;
}

[data-theme='light'] {
  --theme-logo: './logo_light.png';
  --theme-logo-inv: './logo_dark.png';
  --is-dark: 0;
  --is-white: 1;
  --bg0: #ececec;
  --bg50: #ececec88;
  --bg2: #dbdbdb;

  --color-op: #ffffff;
  --color0: #000000;
  --color50: #00000088;

  --color1: #0b0805;
  --color2: #575757;
  --color3: #6b6b6b;

  --bborder: rgba(255, 255, 2507 0.3);
  --bbg: rgba(3, 3, 4, 0.5);

  --accent0: #ffcc00;
  --accent50: #ffcc0088;
  --accent1: #0066cc;
  --accent2: hsl(48, 100%, 71%);

  --scrollbar-thumb: rgb(145, 145, 145);
  --scrollbar-track: rgb(242, 242, 242);

  --scrollbar-thumb_hover: rgb(45, 45, 45);
  --scrollbar-track_hover: rgb(226, 226, 226);

  --loader-bg-blend-mode: screen;
}

.theme-toggler {
  background-color: transparent;
  border: none;
  z-index: 1;
  transition: transform 0.5s;
  cursor: pointer;
  opacity: 0.75;
  height: 5rem;
  display: flex;
  align-items: center;
  padding: 0 0.5rem;

  #spot {
    display: flex;
    align-items: center;
    justify-content: center;
    color: var(--color0);
    line-height: 100%;
    width: 3.75rem;
    height: 3.75rem;
    border-radius: 50%;
    background: radial-gradient(
      ellipse at 0% 0%,
      var(--accent2),
      var(--accent1)
    );
  }
}
</style>
