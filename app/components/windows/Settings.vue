<template>
<modal-layout
  :show-cancel="false"
  :done-handler="done"
  class="modal-layout--w-side-menu">

  <div slot="content" class="settings">
    <NavMenu v-model="categoryName">
      <NavItem
        v-for="category in categoryNames"
        :key="category"
        :to="category"
        :ico="icons[category]"
      >
        {{ $t(category) }}
      </NavItem>
    </NavMenu>
    <div class="settings-container" ref="settingsContainer">
      <extra-settings v-if="categoryName === 'General'" />
      <language-settings v-if="categoryName === 'General'" />
      <hotkeys v-if="categoryName === 'Hotkeys'" />
      <developer-settings v-if="categoryName === 'Developer'" />
      <installed-apps v-if="categoryName === 'Installed Apps'" />
      <overlay-settings v-if="categoryName === 'Scene Collections'" />
      <notifications-settings v-if="categoryName === 'Notifications'" />
      <appearance-settings v-if="categoryName === 'Appearance'" />
      <experimental-settings v-if="categoryName === 'Experimental'" />
      <remote-control-settings v-if="categoryName === 'Remote Control'" />
      <game-overlay-settings v-if="categoryName === 'Game Overlay'" />
      <facemask-settings v-if="categoryName === 'Facemasks'" />
      <GenericFormGroups
        v-if="!['Hotkeys', 'API', 'Overlays', 'Notifications', 'Appearance', 'Experimental', 'Remote Control'].includes(categoryName)"
        :categoryName="categoryName"
        v-model="settingsData"
        @input="save" />
    </div>
  </div>
</modal-layout>
</template>

<script lang="ts" src="./Settings.vue.ts"></script>

<style lang="less" scoped>
@import '../../styles/index';

.settings {
  .transition();

  display: flex;
  align-content: stretch;
  align-items: stretch;
  flex: 1;
  margin: -16px;
}

.settings-container {
  .padding-right(2);
  .padding-top(2);

  flex-grow: 1;
  overflow: auto;
}
</style>

<style lang="less">
.settings-container {
  .input-container,
  .alignable-input {
    flex-direction: column;

    .input-label,
    .input-wrapper,
    .input-body {
      width: 100%;
    }

    .bitmask-input > div {
      width: auto;
    }

    .input-label {
      label {
        margin-bottom: 8px;
        line-height: 16px;
      }
    }
  }
}
</style>
