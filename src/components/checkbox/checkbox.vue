<template>
  <label>
    <span>
      <input
        v-if="group"
        type="checkbox"
        :value="label"
        v-model="model"
        :disabled="disabled"
        :checked="currentValue"
        @change="change"
      >
      <input
        v-else
        type="checkbox"
        :disabled="disabled"
        :checked="currentValue"
        @change="change"
      >
    </span>
    <slot></slot>
  </label>
</template>

<script>
import Emitter from '../../mixins/emitter.js';
import { findComponentUpward } from '../../utils/assist.js';

export default {
  name: 'myCheckbox',
  mixins:[Emitter],
  props: {
    disabled: {
      type: Boolean,
      default: false
    },
    value: {
      type: [String, Number, Boolean],
      default: false,
    },
    trueValue: {
      type: [String, Number, Boolean],
      default: true,
    },
    falseValue: {
      type: [String, Number, Boolean],
      default: false,
    },
    label: {
      type: [String, Number, Boolean]
    }
  },
  watch: {
    value(val) {
      if (val === this.trueValue || val === this.falseValue) {
        this.updateModel();
      } else {
        throw 'Value should be trueValue or falseValue.';
      }
    }
  },
  data() {
    return {
      currentValue: this.value,
      model: [],
      group: false,
      parent: null
    };
  },

  mounted() {
    this.parent = findComponentUpward(this, 'myCheckboxGroup');
    if (this.parent) {
      this.group = true;
    }
    if (this.group) {
      this.parent.updateModel(true);
    } else {
      this.updateModel();
    }
  },

  methods: {
    change(event) {
      if (this.disabled) {
        return false;
      }

      const checked = event.target.checked;
      this.currentValue = checked;

      const value = checked ? this.trueValue : this.falseValue;
      this.$emit('input', value);

      if (this.group) {
        this.parent.change(this.model);
      } else {
        this.$emit('on-change', value); 
        this.dispatch('myFormItem', 'on-form-change', value);
      }
    },
    updateModel() {
      this.currentValue = this.value === this.trueValue;
    },
  }
}
</script>

<style lang="scss" scoped>

</style>
