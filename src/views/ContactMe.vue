<template>
  <div class="flex-col-start">
    <div class="flex-col-start page-header padding-13">
      <h2 class="h2" style="left: -0.2rem">
        Contact Me
        <high-light />
      </h2>

      <p class="t2">Hire Me For Your Awesome Project</p>
    </div>

    <div class="flex-col-start">
      <div class="grid-text-form">
        <h2 class="h2">Get in<br />Touch With<br />Me</h2>

        <form @submit.prevent="submitForm" class="flex-col-start form">
          <label data-text="NAME">
            <input
              type="text"
              v-model="name"
              required
              autocomplete="name"
              aria-label="name-input"
            />
          </label>

          <label data-text="EMAIL">
            <input
              type="email"
              v-model="email"
              required
              aria-label="email-input"
            />
          </label>

          <label data-text="SUBJECT">
            <input
              type="text"
              v-model="subject"
              required
              aria-label="subject-input"
            />
          </label>

          <label data-text="MESSAGE">
            <textarea v-model="message"></textarea>
          </label>

          <active-element
            :padding="'0'"
            :fontSize="'2.1rem'"
            :borderRadius="'1.75rem'"
            :bg="'var(--accent0)'"
            class="font-variant"
          >
            send
          </active-element>
        </form>
      </div>
    </div>

    <div class="laptop"></div>

    <div class="address">
      <h4 class="h4">
        <a
          href="https://t.me/bogdanovvad1m"
          class="link"
          style="padding: 0.5rem; margin: -0.5rem"
          title="Contact me via Telegram or any other social media"
        >
          @bogdanovvad1m
        </a>
      </h4>

      <h4 class="h4">
        <a
          href="tel:+380505444199"
          class="link"
          style="padding: 0.5rem; margin: -0.5rem"
          title="Contact me via phone"
        >
          +380-505-444-199
        </a>
      </h4>

      <h4 class="h4">
        <a
          href="mailto:8ogdanow@gmail.com"
          class="link"
          style="padding: 0.5rem; margin: -0.5rem"
          title="Contact me via e-mail"
        >
          8ogdanow@gmail.com
        </a>
      </h4>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import HighLight from '@/components/HighLight.vue'
import ActiveElement from '@/components/ActiveElement.vue'
import emailjs from 'emailjs-com'

const name = ref('')
const email = ref('')
const subject = ref('')
const message = ref('')

const SERVICE_ID = import.meta.env.VITE_EMAILER_SERVICE_ID
const TEMPLATE_ID = import.meta.env.VITE_EMAILER_TEMPLATE_ID
const USER_KEY = import.meta.env.VITE_EMAILER_USER_KEY

const submitForm = async () => {
  const text = `
        Name: ${name.value}
        Email: ${email.value}
        Subject: ${subject.value}
        Message: ${message.value}
      `

  try {
    const templateParams = {
      name: name.value,
      email: email.value,
      subject: subject.value,
      message: text.trim(),
    }

    const response = await emailjs.send(
      SERVICE_ID,
      TEMPLATE_ID,
      templateParams,
      USER_KEY
    )
    console.log('Email sent successfully!', response)
  } catch (error) {
    console.error('Error sending email:', error)
  }

  name.value = ''
  email.value = ''
  subject.value = ''
  message.value = ''
}

onMounted(() => window.scrollTo(0, 0))
</script>

<style lang="scss" scoped>
.grid-text-form {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 7rem;
  padding: 9.5rem 0 7.25rem 0;
}

.form {
  font-family: 'Rubik', sans-serif;
  gap: 3.5rem;
  font-size: 1.5rem;
  font-weight: 400;
  color: var(--color0) !important;

  label {
    position: relative;
    background: transparent !important;

    &::before {
      position: absolute;
      left: 0;
      top: 0;
      height: 2rem;
      width: 5rem;
      content: attr(data-text);
      line-height: 1.5rem;
    }
  }
}

*:focus {
  outline: none;
  font-size: 1.5rem;
}
.form *:not([type='submit']) {
  width: 100%;
  height: 5rem;
  background: transparent !important;
  border-width: 0.125rem;
  border-color: transparent transparent var(--color2) transparent;
  color: var(--color0);
  display: inline-flex;
  align-items: flex-end;
  overflow: hidden;

  &:focus {
    outline: none;
    border: none none auto none;
  }

  input {
    padding: 2.5rem 0 1rem 0;
  }

  textarea {
    padding: 2rem 0 0rem 0;
  }

  input,
  textarea {
    font-family: 'Victor Mono', monospace;
    font-size: 1.5rem;

    &:not(:focus) {
      font-weight: 500;
    }

    &:focus {
      font-weight: 400;
      font-style: italic;
    }
  }
}

input[type='submit'],
button {
  width: 11rem;
  height: 3.5rem;
  background: var(--accent0);
  border-color: transparent;
  border-radius: 1.75rem;
  border-width: 0.125rem;
  padding: 0;
  margin: 0;
  position: relative;
  color: var(--color0);
  box-sizing: content-box;
  cursor: pointer;
  font-weight: 400;
}

input:-webkit-autofill,
input:-webkit-autofill:hover,
input:-webkit-autofill:focus,
input:-webkit-autofill:active {
  transition: background-color 5000s;
  -webkit-text-fill-color: var(--color0) !important;
  -webkit-background-clip: text !important;
  background-clip: text !important;
  font-size: 1.5rem;
}

textarea {
  resize: none;
  font-size: 1.5rem;
}

.laptop {
  border-radius: 1rem;
  background-image: url('@/assets/laptop.webp');
  width: 100%;
  height: 55.5%;
  background-size: cover;
  background-position: center;
  background-repeat: no-repeat;
  aspect-ratio: 1148 / 636;
  margin-bottom: 6.25rem;
}

.address {
  display: flex;
  align-items: center;
  justify-content: space-around;
  gap: 3rem;
  margin-bottom: 10rem;
}
</style>
