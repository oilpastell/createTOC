<template>
  <div class="toc-catalogue"></div>
</template>

<script>
export default {
  name: "Catalogue",
  data() {
    return {};
  },
  mounted() {
    this.init();
    window.addEventListener("resize", this.observer);
  },
  beforeDestroy() {
    window.removeEventListener("resize", this.observer);
    window.removeEventListener("scroll", this.toActive);
  },
  computed: {},
  methods: {
    init() {
      this.getCatalogue();
      this.observer();
    },
    getCatalogue() {
      let tocList = document.querySelectorAll(".toc-item");
      let str = ``;
      Array.from(tocList, (v) => {
        const titleNode = document.querySelector(`#${v.id} .toc-head-title`);
        str += `
    			<span id="${v.id}" class="toc-catalogue-item">${titleNode.textContent}</span>
    		\n`;
      });
      let toc = document.querySelector(".toc-catalogue");
      toc.innerHTML = "";
      toc.insertAdjacentHTML("beforeend", str);
      this.setEvent(tocList);
    },
    setEvent(tocList) {
      Array.from(tocList, (v) => {
        const btn = document.querySelector(`.toc-catalogue #${v.id}`);
        const ele = document.querySelector(`.toc-contain #${v.id} .point`);
        if (!btn || !ele) return;
        btn.addEventListener("click", () => {
          ele.scrollIntoView({
            block: "start",
            behavior: "smooth",
          });
        });
      });
    },
    toActive() {
      const sections = document.querySelectorAll(".point");
      const tocLinks = document.querySelectorAll(".toc-catalogue span");
      if (!tocLinks.length || !sections.length) {
        return;
      }
      let currentSectionIndex = 0;

      for (let i = 0; i < sections.length; i++) {
        if (sections[i].getBoundingClientRect().top <= 2) {
          currentSectionIndex = i;
        }
      }

      for (let i = 0; i < tocLinks.length; i++) {
        tocLinks[i].classList.remove("toc-catalogue-active");
      }

      tocLinks[currentSectionIndex].classList.add("toc-catalogue-active");
    },
    observer() {
      this.toActive();
      window.addEventListener("scroll", this.toActive, true);
    },
  },
};
</script>

<style lang="scss" scoped>
.toc-catalogue {
  position: fixed;
  right: 0;
  top: 50%;
  transform: translateY(-50%);
  height: fit-content;
  padding: 16px;
  font-size: 14px;
  color: #666666;
  font-family: "PingFang SC";
  background-color: #fff;
  display: flex;
  flex-direction: column;
  border-radius: 4px 0 0 4px;
  box-shadow: 0px 4px 20px 0px rgba(51, 51, 51, 0.12);
  ::v-deep .toc-catalogue-active {
    color: #1472ff;
    font-weight: 500;
  }
  ::v-deep .toc-catalogue-item {
    cursor: pointer;
    &:not(:last-child) {
      margin-bottom: 32px;
    }
  }
}
</style>
