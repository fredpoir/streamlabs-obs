
<template>
<div class="live-container">
  <div class="flex__column">
    <div class="flex__item mission-control-container">
      <browser-view
        class="mission-control"
        :hidden="windowsService.state.main.hideStyleBlockers"
        :src="recenteventsUrl"
        :setLocale="true"
        @ready="onBrowserViewReady" />
    </div>
    <resize-bar
      class="flex__item live-page-resizer"
      position="top"
      v-model="height"
      @onresizestop="onResizeStopHandler()"
      @onresizestart="onResizeStartHandler()"
      :max="maxHeight"
      :min="minHeight"
      :reverse="true"
    />
    <div
      class="flex__item studio-controls"
      :style="{ flex: '0 0 ' + (height) + 'px' }">
      <scene-selector class="studio-controls-panel" />

      <mixer class="studio-controls-panel" />

      <div class="live-preview-container" :style="{ flex: '0 1 ' + displayWidth + 'px' }">
        <div class="studio-controls-top">
          <h4 class="studio-controls__label">
            {{ $t('Preview') }}
          </h4>
          <div v-if="!performanceModeEnabled">
            <i
              v-if="previewEnabled"
              class="icon-view icon-button icon-button--lg"
              @click="previewEnabled = false"
              v-tooltip="disablePreviewTooltip"/>
            <i
              v-if="!previewEnabled"
              class="icon-hide icon-button icon-button--lg"
              @click="previewEnabled = true"
              v-tooltip="enablePreviewTooltip"/>
          </div>
        </div>

        <div class="live-display-wrapper">
          <display class="live-display" :drawUI="false" v-if="previewEnabled" />
          <div class="live-display-placeholder" v-else>
            <img class="live-display-placeholder__img" :src="sleepingKevin">
            <span v-if="!performanceModeEnabled">{{ $t('Your preview is currently disabled') }}</span>
            <span v-if="performanceModeEnabled">{{ $t('Preview is disabled in performance mode') }}</span>
          </div>
        </div>
      </div>
    </div>
  </div>
</div>
</template>

<script lang="ts" src="./Live.vue.ts"></script>

<style lang="less" scoped>
@import '../../styles/index';

.live-container {
  .padding(2);

  display: flex;
  height: 100%;
  width: 100%;
  box-sizing: border-box;
}

.mission-control-container {
  .radius();

  flex: 1;
  overflow: hidden;
  position: relative;
}

.mission-control {
  height: 100%;
}

.mission-control.hidden {
  position: absolute;
  top: -10000px;
}

.studio-controls {
  display: flex;
  position: relative;
  flex: 0 0 208px;
}

.studio-controls-panel {
  flex-grow: 1;
  padding-left: 0;
  .padding-right(2);
}

.live-page-resizer {
  margin: 4px 0;
}

.live-preview-container {
  flex: 0 0 auto;
}

.live-display-wrapper {
  .radius();
  .border();

  max-width: 100%;
  background-color: var(--section);
  position: relative;
  border-top: 0;
  height: calc(~'100% - 29px');
}

.live-display-placeholder {
  height: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  background: var(--section);

  span {
    color: var(--icon);
    font-size: 12px;
  }
}

.live-display-placeholder__img {
  margin-bottom: 20px;
  width: 40%;
}
</style>
