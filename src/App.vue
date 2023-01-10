<template>
  <HeaderView />
  <BodyView />
</template>

<script>
import HeaderView from "./layouts/TheHeader.vue";
import BodyView from "./layouts/TheBody.vue";
export default {
  name: "App",
  components: { HeaderView, BodyView },
};
</script>

<style scoped></style>
