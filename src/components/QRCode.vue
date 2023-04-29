<template>
  <div class="wrapper">
    <header>
      <h1>QR CODE GENERATOR</h1>
    </header>
    <form>
      <p>Paste a url to create QR code</p>
      <input
        type="text"
        name="input-link"
        placeholder="Enter your url"
        v-model="inputURL"
        v-on:keyup="if (!inputURL) showQRCode = false;"
      />
      <button @click.prevent="handleQRCode" class="btn-generate">
        Generate QR code
      </button>
    </form>
    <div :class="`qr-code ${showQRCode ? 'active' : ''}`">
      <img src="result" alt="QR code" />
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";

const showQRCode = ref(false);
const inputURL = ref("");

const handleQRCode = () => {
  const wrapper = document.querySelector(".wrapper");
  const image = wrapper.querySelector("img");

  if (inputURL.value) {
    image.src = `https://api.qrserver.com/v1/create-qr-code/?size=200x200&data=${inputURL.value}`;

    return (showQRCode.value = true);
  }
};
// API : https://goqr.me/api/
</script>
