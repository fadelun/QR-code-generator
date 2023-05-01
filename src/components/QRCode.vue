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
      <div class="option">
        <div class="input-color flex items-center w-2/4">
          <label for="color">color</label>
          <input
            type="color"
            name="color"
            id="color"
            v-model="inputColor"
            @change="check"
          />
        </div>
        <div class="input-bgcolor">
          <label for="bgcolor">bgcolor</label>
          <input
            type="color"
            name="bgcolor"
            id="bgcolor"
            v-model="inputBgcolor"
            @change="check"
          />
        </div>
      </div>
      <button @click.prevent="handleQRCode" class="btn-generate">
        Generate QR code
      </button>
    </form>
    <div :class="`qr-code ${showQRCode ? 'active' : ''}`">
      <img src="result" alt="QR code" :class="{ hidden: !showQRCode }" />
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";

const showQRCode = ref(false);
const inputURL = ref("");
const inputColor = ref("");
const inputBgcolor = ref("");

const check = (e) => {
  return e.target.value;
};

const handleQRCode = () => {
  const wrapper = document.querySelector(".wrapper");
  const image = wrapper.querySelector("img");

  if (inputURL.value) {
    image.src = `https://api.qrserver.com/v1/create-qr-code/?size=400x400&data=${
      inputURL.value
    }&color=${inputColor.value.substr(1)}&bgcolor=${inputBgcolor.value.substr(
      1,
    )}
    `;

    return (showQRCode.value = true);
  }
};
// API : https://goqr.me/api/
</script>
