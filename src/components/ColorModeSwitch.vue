<template>
  <i
    class="fa-solid color-mode-switch"
    :class="[isDarkMode ? 'fa-toggle-on' : 'fa-toggle-off']"
    @click="switchColorMode"
  />
</template>

<script lang="ts">
import { defineComponent, PropType, ref } from "vue";

// types
import { Color } from "@/types/Color";

export default defineComponent({
  name: "ColorModeSwitch",
  props: {
    colors: {
      type: Array as PropType<Color[]>,
      default: () => [],
    },
  },
  setup(props) {
    const isDarkModeLocalStorageKey = "isDarkMode";

    const isDarkMode = ref(
      JSON.parse(
        window?.localStorage?.getItem(isDarkModeLocalStorageKey) ?? "false"
      )
    );

    const switchColorMode = () => {
      isDarkMode.value = !isDarkMode.value;
      window?.localStorage?.setItem(
        isDarkModeLocalStorageKey,
        JSON.stringify(isDarkMode.value)
      );

      setVariableValues();
    };

    const setVariableValues = () => {
      if (isDarkMode.value) {
        props.colors.forEach((color) =>
          document.documentElement.style.setProperty(
            color.variableName,
            color.darkModeValue
          )
        );
      } else {
        props.colors.forEach((color) =>
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
  user-select: none;
  cursor: pointer;
}
</style>
