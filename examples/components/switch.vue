<template>
  <label
    class="hy-switch"
    @click="handleClick"
    :class="{ 'is-checked': value }"
    :for="name"
  >
    <input
      class="hy-switch__input"
      type="checkbox"
      :name="name"
      :checked="value"
    />
    <span class="hy-switch__core" ref="core">
      <span class="hy-switch__button"></span>
    </span>
  </label>
</template>

<script>
export default {
  name: 'HySwitch',
  props: {
    value: {
      type: Boolean,
      default: false
    },
    activeColor: {
      type: String,
      default: ''
    },
    inactiveColor: {
      type: String,
      default: ''
    },
    name: {
      type: String,
      default: ''
    }
  },
  methods: {
    async handleClick () {
      this.$emit('input', !this.value)
      // 改变input框的值
      // 等待value发生改变后，再setColor
      // 数据修改后，等待DOM更新，再修改按钮的颜色
      await this.$nextTick()
      this.setColor()
    },
    setColor () {
      if (this.activeColor || this.inactiveColor) {
        const color = this.value ? this.activeColor : this.inactiveColor
        this.$refs.core.style.borderColor = color
        this.$refs.core.style.backgroundColor = color
      }
    }
  },
  mounted () {
    // 页面一进入调用
    // 设置颜色
    this.setColor()
  }
}
</script>

<style lang='scss' scoped>
.hy-switch {
  display: inline-flex;
  align-items: center;
  position: relative;
  font-size: 14px;
  line-height: 20px;
  height: 20px;
  vertical-align: middle;
  &__input {
    position: absolute;
    width: 0;
    height: 0;
    opacity: 0;
    margin: 0;
  }
  &__core {
    margin: 0;
    display: inline-block;
    position: relative;
    width: 40px;
    height: 20px;
    border: 1px solid #dcdfe6;
    outline: none;
    border-radius: 10px;
    box-sizing: border-box;
    background: #dcdfe6;
    cursor: pointer;
    transition: all 0.3s;
    // transition: border-color 0.3s, background-color 0.3s;
    vertical-align: middle;
    .hy-switch__button {
      position: absolute;
      top: 1px;
      left: 1px;
      border-radius: 100%;
      transition: all 0.3s;
      width: 16px;
      height: 16px;
      background-color: #fff;
    }
  }
}
.hy-switch.is-checked {
  .hy-switch__core {
    border-color: #409eff;
    background-color: #409eff;
    .hy-switch__button {
      transform: translateX(20px);
    }
  }
}
</style>
