<template lang="html">
  <div class="split-container">
    <button
      class="split-tab-button"
      :class="isActive('example')"
      type="button"
      @click="setDisplay('example')"
    >
      Example
    </button>
    <button
      class="split-tab-button"
      :class="isActive('code')"
      type="button"
      @click="setDisplay('code')"
    >
      Code
    </button>
    <button
      class="split-tab-button"
      :class="isActive('both')"
      type="button"
      @click="setDisplay('both')"
    >
      Example+Code
    </button>
    <div class="split">
      <div
        v-if="exampleVisible"
        class="split-example"
      >
        <keep-alive>
          <slot name="example"/>
        </keep-alive>
      </div>
      <div
        v-if="codeVisible"
        class="split-code"
      >
        <slot/>
      </div>
    </div>
  </div>
</template>

<script>
import Vue from 'vue'

export default Vue.extend({
  data() {
    return {
      display: this.active,
    }
  },
  props: {
    active: {
      type: String,
      default: 'example',
    },
  },
  computed: {
    exampleVisible() {
      return this.display === 'example' || this.display === 'both'
    },
    codeVisible() {
      return this.display === 'code' || this.display === 'both'
    },
  },
  methods: {
    /**
     * @param {string} type
     */
    setDisplay(type) {
      this.display = type
    },
    /**
     * @param {string} type
     */
    isActive(type) {
      return this.display === type ? 'split-tab-button-active' : ''
    },
  },
})
</script>

<style lang="stylus" scoped>
.split-container {
  margin: 20px 0;
  padding: 20px;
  background: #EEE;
  border-radius: 5px;
}

.split-tab-button {
  border: none;
  background: #fff;
  padding: 12px 24px;
  font-size: 14px;
  display: inline-flex;
  margin-bottom: 5px;
}

.split-tab-button-active {
  color: #fff;
  background: #3eaf7c;
}

.split {
  background-color: white;
  border-radius: 5px;
  width: auto;
  display: flex;
  margin: 0 -10px;

  & > div {
    padding: 0 10px;
    flex-grow: 1;
    width: 50%;
  }
}

.split-example {
  margin: 0.85rem 0;
}
</style>
