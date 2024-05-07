<template>
  <div class="toc-item" :id="'toc-' + TOCId">
    <div class="point" style="position: absolute;top: -72px;"></div>
    <div class="toc-head">
      <span class="split-box"></span>
      <span class="toc-head-title">{{ title }}</span>
      <ss-popover trigger="hover" :placement="placement">
        <div slot="default">
          <span v-if="!useIconTipsSlot && iconTips">{{iconTips}}</span>
          <slot name="icon-tips" v-else></slot>
        </div>
        <i
          class="sense-icon-info-stroke"
          style="color: #999; margin-left: 4px; cursor: pointer"
          slot="reference"
          v-show="iconTips || useIconTipsSlot"
        ></i>
      </ss-popover>
      <a
        :href="linkTips.link"
        style="color: #1472ff; margin-left: 8px"
        v-if="linkTips.tips"
        target="_black"
      >{{ linkTips.tips }}</a>
      <span style="color: #999999; margin-left: 8px" v-if="textTips">{{ textTips }}</span>
    </div>
    <slot></slot>
  </div>
</template>

<script>
import { Popover } from '@xiaoe/sense';
export default {
  name: 'TOCItem',
  components: {
    [Popover.name]: Popover
  },
  props: {
    title: {
      type: String,
      default: ''
    },
    textTips: {
      type: String,
      default: ''
    },
    iconTips: {
      type: String,
      default: ''
    },
    placement: {
      type: String,
      default: 'top'
    },
    useIconTipsSlot: {
      type: Boolean,
      default: false
    },
    linkTips: {
      type: Object,
      default: () => {
        return {
          link: '',
          tips: ''
        };
      }
    }
  },
  data() {
    return {};
  },
  beforeCreate() {
    this.$parent.items.push(this);
  },
  beforeDestroy() {
    const items = this.$parent.items;
    const index = items.indexOf(this);
    if (index >= 0) {
      items.splice(index, 1);
    }
  },
  computed: {
    TOCId() {
      return this.$parent.items?.indexOf(this) + 1;
    }
  },
  methods: {}
};
</script>

<style lang="scss" scoped>
.toc-item {
  padding: 16px;
  background-color: #fff;
  font-family: 'PingFang SC';
  position: relative;
  &:not(:last-child) {
    margin-bottom: 16px;
  }
  .toc-head {
    display: flex;
    align-items: center;
    margin-bottom: 24px;
  }
  .toc-head-title {
    color: #333333;
    font-weight: 500;
    line-height: 24px;
    font-size: 16px;
  }
  .split-box {
    display: inline-block;
    width: 2px;
    height: 14px;
    border-radius: 16px;
    opacity: 1;
    background: #1472ff;
    margin-right: 8px;
  }
}
</style>
