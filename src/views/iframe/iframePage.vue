<template>
  <div :class="[fullScreen ? 'iframe-container-full' : 'iframe-container-no-full']">
    <div class="title-bar">
      <h3>{{ title }}</h3>
      <div>
        <a-tooltip>
          <template slot="title">
            {{ !fullScreen ? '展开' : '还原' }}
          </template>
          <a-icon v-if="!fullScreen" @click="toggleFull" class="fullscreen-icon" type="fullscreen"/>
          <a-icon v-else @click="toggleFull" class="fullscreen-icon" type="fullscreen-exit"/>
        </a-tooltip>
      </div>
    </div>
    <iframe
      v-if="url !== undefined"
      class="iframe"
      :style="{minHeight: `calc(100vh - 64px)`}"
      :src="url"
      width="100%"
      height="100%"
    />
    <div v-else class="bgw">
      <a-empty/>
    </div>
  </div>
</template>

<script>
  import { getQueryVariable } from '@/utils/util'
  import Empty from 'ant-design-vue/es/empty'

  export default {
    name: 'IframeLayout',
    components: { 'a-empty': Empty },
    data: () => {
      return {
        url: getQueryVariable('url'),
        title: getQueryVariable('title'),
        fullScreen: false
      }
    },
    methods: {
      toggleFull (e) {
        e.preventDefault()
        this.fullScreen = !this.fullScreen
      }
    }
  }
</script>

<style lang="less" scoped>
  .bgw{
    background-color: white;
    padding: 20px;
  }
  .iframe-container-full {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    z-index: 999;
  }

  .iframe {
    border: none;
  }

  .title-bar {
    background-color: #fff;
    padding: 8px 16px 8px 8px;
    display: flex;
    align-items: center;
    border-bottom: 1px solid #ccc;

    h3 {
      margin: 0;
      flex: 1;
    }

    .fullscreen-icon {
      font-size: 20px;
      cursor: pointer;
    }
  }
</style>
