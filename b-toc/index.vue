<template>
  <div class="toc">
    <div class="toc-contain" id="toc-contain">
      <slot></slot>
    </div>
    <Catalogue ref="Catalogue"></Catalogue>
  </div>
</template>

<script>
import Catalogue from "./Catalogue/index.vue";
export default {
  name: "TOC",
  components: {
    Catalogue,
  },
  data() {
    return {
      items: [],
    };
  },
  computed: {},
  methods: {},
  updated() {
    this.$refs.Catalogue.init();
  },
};
</script>

<style lang="scss" scoped>
.toc {
  width: 100%;
  height: 100%;
  .toc-contain {
    width: 100%;
    height: 100%;
  }
}
</style>
