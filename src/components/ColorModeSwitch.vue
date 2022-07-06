<template>
  <i
    class="fa-solid color-mode-switch"
    :class="[isDarkMode ? 'fa-toggle-on' : 'fa-toggle-off']"
    @click="switchColorMode"
  />
</template>

<script lang="ts">
import { defineComponent, ref } from "vue";

import { colors } from "@/colors";

export default defineComponent({
  name: "ColorModeSwitch",
  setup() {
    const isDarkModeLocalStorageKey = "isDarkMode";

    const isDarkMode = ref(
      JSON.parse(localStorage.getItem(isDarkModeLocalStorageKey) ?? "false")
    );

    const switchColorMode = () => {
      isDarkMode.value = !isDarkMode.value;
      localStorage.setItem(
        isDarkModeLocalStorageKey,
        JSON.stringify(isDarkMode.value)
      );

      setVariableValues();
    };

    const setVariableValues = () => {
      if (isDarkMode.value) {
        colors.forEach((color) =>
          document.documentElement.style.setProperty(
            color.variableName,
            color.darkModeValue
          )
        );
      } else {
        colors.forEach((color) =>
          document.documentElement.style.setProperty(
            color.variableName,
            color.lightModeValue
          )
        );
      }
    };

    setVariableValues();

    return {
      isDarkMode,
      switchColorMode,
    };
  },
});
</script>

<style lang="scss" scoped>
.color-mode-switch {
  font-size: 4rem;
  color: var(--primary-text-color);
  cursor: pointer;
}
</style>
