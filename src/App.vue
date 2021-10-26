<template>
  <theme-button />
  <router-view />
</template>

<script lang="ts">
import ThemeButton from "./components/forms/ThemeButton.vue";

export default {
  components: {
    ThemeButton,
  },
};
</script>

<style src="@/assets/sass/style.scss" lang="scss" />
