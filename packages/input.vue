<template>
  <div class="hy-input" :class="{ 'hy-input--suffix': showSuffix }">
    <input
      class="hy-input__inner"
      :class="{ 'is-disabled': disabled }"
      :placeholder="placeholder"
      :type="showPassword ? (passwordVisible ? 'text' : 'password') : type"
      :name="name"
      :disabled="disabled"
      :value="value"
      @input="handleInput"
    />
    <span class="hy-input__suffix" v-if="showSuffix">
      <i
        class="hy-input__icon hy-icon-close"
        v-if="clearable && value"
        @click="clear"
      ></i>
      <i
        class="hy-input__icon hy-icon-pacman"
        :class="{ 'hy-icon-pacman__active': passwordVisible }"
        v-if="showPassword && value"
        @click="handlePassword"
      ></i>
    </span>
  </div>
</template>

<script>
export default {
  name: 'HyInput',
  data () {
    return {
      // 是否显示密码
      passwordVisible: false
    }
  },
  props: {
    placeholder: {
      type: String,
      default: ''
    },
    type: {
      type: String,
      default: 'text'
    },
    name: {
      type: String,
      default: ''
    },
    disabled: {
      type: Boolean,
      default: false
    },
    value: {
      type: String,
      default: ''
    },
    clearable: {
      type: Boolean,
      default: false
    },
    showPassword: {
      type: Boolean,
      default: false
    }
  },
  created () {
    // console.log(this.placeholder)
  },
  methods: {
    handleInput (e) {
      this.$emit('input', e.target.value)
      // this.$emit('update:value', e.target.value)
    },
    clear () {
      this.$emit('input', '')
    },
    handlePassword () {
      this.passwordVisible = !this.passwordVisible
    }
  },
  computed: {
    showSuffix () {
      return this.clearable || this.showPassword
    }
  }
}
</script>

<style lang='scss' scoped>
.hy-input {
  width: 100%;
  position: relative;
  font-size: 14px;
  display: inline-block;
  .hy-input__inner {
    -webkit-appearance: none;
    background-color: #fff;
    background-image: none;
    border-radius: 4px;
    border: 1px solid #dcdfe6;
    box-sizing: border-box;
    color: #606266;
    display: inline-block;
    font-size: inherit;
    height: 40px;
    line-height: 40px;
    outline: none;
    padding: 0 15px;
    transition: border-color 0.2s cubic-bezier(0.645, 0.045, 0.355, 1);
    width: 100%;

    &:focus {
      outline: none;
      border-color: #409eff;
    }
    &.is-disabled {
      background-color: #f5f7fa;
      border-color: #e4e7ed;
      color: #c0c4cc;
      cursor: not-allowed;
    }
  }
}
.hy-input--suffix {
  .hy-input__inner {
    padding-right: 30px;
  }
  .hy-input__suffix {
    position: absolute;
    height: 100%;
    right: 10px;
    top: 0;
    line-height: 40px;
    text-align: center;
    color: #c0c4cc;
    transition: all 0.3s;
    z-index: 900;
    i {
      color: #c0c4cc;
      font-size: 14px;
      cursor: pointer;
      transition: color 0.2s cubic-bezier(0.645, 0.045, 0.355, 1);
    }
    .hy-icon-pacman.hy-icon-pacman__active {
      color: #747475;
    }
  }
}
</style>
