<template>
  <div class="container">
    <ColorModeSwitch />
    <h1>Color Mode Switch!</h1>
    <p>
      Lorem ipsum dolor sit, amet consectetur adipisicing elit. Molestias,
      minus. Ab, quasi explicabo vitae ratione aliquam dolor delectus obcaecati
      quas. Quas dolor maxime aut iure blanditiis cum porro iste exercitationem!
    </p>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";

// components
import ColorModeSwitch from "@/components/ColorModeSwitch.vue";

export default defineComponent({
  name: "App",
  components: {
    ColorModeSwitch,
  },
});
</script>

<style lang="scss" scoped>
.container {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  min-height: 100vh;
  padding: 0 1rem;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 2rem;
  background-color: var(--primary-background-color);

  h1 {
    color: var(--primary-text-color);
    text-align: center;
    font-size: 4rem;
    margin: 0;

    @media only screen and (min-width: 920px) {
      font-size: 8rem;
    }
  }

  p {
    color: var(--primary-text-color);
    text-align: center;
    max-width: 40rem;
  }
}
</style>
