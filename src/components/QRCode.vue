<template>
  <div class="wrapper">
    <header>
      <h1>QR CODE GENERATOR</h1>
    </header>
    <form>
      <p>Paste a url to create QR code</p>
      <input type="text" name="input-link" placeholder="Enter your url" />
      <button
        @click.prevent="() => (showQRCode = !showQRCode)"
        class="btn-generate"
      >
        Generate QR code
      </button>
    </form>
    <div :class="`qr-code ${showQRCode ? 'active' : ''}`">
      <img src="./../assets/QR_code.png" alt="QR code" />
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";

const showQRCode = ref(false);
</script>
