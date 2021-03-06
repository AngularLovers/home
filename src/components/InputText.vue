<template>
  <InputBase class="InputText u-relative" :name="name" :label="label" :error="!!error">
    <input
      :id="name"
      class="input"
      :type="type"
      :name="name"
      :placeholder="placeholder"
      :value="value"
      @input="$emit('input', $event.target.value)"
      @blur="$emit('blur')"
    >
    <transition name="fade">
      <p v-if="error" class="error">
        {{ error }}
      </p>
    </transition>
  </InputBase>
</template>

<script lang="ts">
import Vue from 'vue'
import InputBase from './InputBase.vue'

export default Vue.extend({
  components: {
    InputBase
  },

  props: {
    type: { type: String, default: 'text' },
    name: { type: String, required: true },
    label: { type: String, required: true },
    placeholder: { type: String, required: true },
    value: { type: String, required: true },
    error: { type: String, default: null }
  }
})
</script>

<style lang="postcss" scoped>
@import '@/assets/styles/variables';

.InputText.has-error {
  .input {
    border-color: var(--c-danger);
  }
}

.input {
  width: 100%;
  padding: 11px 16px;
  background-color: var(--c-white-mute);
  border: 1px solid transparent;
  border-radius: 4px;
  transition: border-color 0.25s, background-color 0.25s, color 0.25s;

  &::placeholder {
    color: var(--c-gray-light);
  }

  &:hover,
  &:focus {
    border-color: var(--c-vue-green);
  }

  &:focus {
    background-color: var(--c-white);
  }
}

.error {
  position: absolute;
  bottom: -24px;
  left: 0;
  padding-left: 4px;
  font-size: 12px;
  line-height: 20px;
  color: var(--c-danger);
}

.error.fade-enter-active,
.error.fade-leave-active {
  transition: opacity 0.25s, transform 0.25s;
}

.error.fade-enter,
.error.fade-leave-to {
  opacity: 0;
  transform: translateX(-4px);
}
</style>
