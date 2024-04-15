<template>
  <button class="copy-button" @click="copyButtonClicked">
    {{ this.buttonText }}
  </button>
</template>
<script>
export default {
  data() {
    return {
      buttonText: "📄 Copy",
      copyText:
        '<script src="https://cdn.jsdelivr.net/gh/dotmaz/preservejs@latest/preserve.js"><' +
        "/" +
        "script>",
    };
  },
  methods: {
    copyButtonClicked() {
      this.buttonText = "📄 Copied ✔";
      this.copyToClipboard(this.copyText);
    },
    copyToClipboard(text) {
      const element = document.createElement("textarea");
      element.value = text;
      document.body.appendChild(element);
      element.select();
      document.execCommand("copy");
      document.body.removeChild(element);
    },
  },
};
</script>
<style scoped>
.copy-button {
  font-family: "Montserrat" !important;
  background: rgba(255, 255, 255, 0.1);
  border: 2px solid #fff;
  color: #fff;
  font-weight: bold;
  font-size: 15px;
  border-radius: 3px;
  padding: 4px 8px;
  cursor: pointer;
  transition-duration: 50ms;

  &:hover {
    background: rgba(255, 255, 255, 0.3);
  }

  &:active {
    transform: scale(0.98);
  }
}
</style>
