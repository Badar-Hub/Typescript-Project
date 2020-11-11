<template>
  <label for="_button" :class="{'active': isActive}" class="toggle__button">
    <span v-if="isActive" class="toggle__label">{{ enableText }}</span>
    <span v-if="! isActive" class="toggle__label">{{ disableText }}</span>

    <input type="checkbox" id="_button" v-model="checkedValue" />
    <span class="toggle__switch"></span>
  </label>
</template>

<script lang="ts">
import { Component, Vue, Prop, Emit, Watch } from "vue-property-decorator";

@Component
export default class ToggleButton extends Vue {
  @Prop({ default: false })
  disabled!: boolean;

  @Prop({ default: false })
  defaultState!: boolean;

  @Prop({ default: "On" })
  labelEnableText!: string;

  @Prop({ default: "Off" })
  labelDisableText!: string;

  @Emit()
  change(): boolean {
    return this.currentState;
  }

  /**
   * Initial data
   */

  currentState: boolean = this.defaultState;

  get isActive(): boolean {
    return this.currentState;
  }

  get enableText(): string {
    return this.labelEnableText;
  }

  get disableText(): string {
    return this.labelDisableText;
  }

  get checkedValue(): boolean {
    return this.currentState;
  }

  set checkedValue(newValue) {
    this.currentState = newValue;
  }

  @Watch("defaultState")
  onPropertyChanged() {
    this.currentState = this.defaultState;
  }
}
</script>

<style lang="scss" scoped>
$base-darken: #666666;
$base-active-darken: #53b883;

.toggle__button {
  vertical-align: middle;
  user-select: none;
  cursor: pointer;

  input[type="checkbox"] {
    opacity: 0;
    position: absolute;
    width: 1px;
    height: 1px;
  }

  .toggle__switch {
    display: inline-block;
    height: 12px;
    border-radius: 6px;
    width: 40px;
    background: rgba($base-darken, 0.2);
    box-shadow: inset 0 0 1px rgba($base-darken, 0.2);
    position: relative;
    margin-left: 10px;
    transition: all 0.25s;

    &::after,
    &::before {
      content: "";
      position: absolute;
      display: block;
      height: 18px;
      width: 18px;
      border-radius: 50%;
      left: 0;
      top: -3px;
      transform: translateX(0);
      transition: all 0.25s cubic-bezier(0.5, -0.6, 0.5, 1.6);
    }

    &::after {
      background: $base-darken;
      box-shadow: 0 0 1px $base-darken;
    }

    &::before {
      background: $base-darken;
      box-shadow: 0 0 0 3px rgba($base-darken, 0.1);
      opacity: 0;
    }
  }
}

.active {
  .toggle__switch {
    background: rgba($base-active-darken, 0.2);
    box-shadow: inset 0 0 1px rgba($base-active-darken, 0.2);

    &::before,
    &::after {
      transform: translateX(0px);
    }

    &::after {
      left: 23px;
      background: $base-active-darken;
      box-shadow: 0 0 1px $base-active-darken;
    }
  }
}
</style>