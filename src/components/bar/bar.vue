<template>
    <div class="bar">
      <div v-for="index in num" class="unit" ref="units" @click.stop.prevent="goto(index-1)" :class="{inverse: inverseControl && centerIndex === index-1, centerFont: centerIndex === index-1}">
        <span class="icon-spinner11"></span>
      </div>
    </div>
</template>

<script>
    export default {
      props: {
        num: {
          type: Number,
          default: 0
        }
      },
      data() {
        return {
          centerIndex: 0,
          inverseControl: false
        }
      },
      methods: {
        /**
         * 点击小圆点跳转到指定图片
         * @param index 点击的小圆点的索引
         */
        goto: function(index) {
          this.$emit('goto', index);
        },
        /**
         * 供父组件使用，改变inverseControl
         * */
        changeIndexControl: function () {
          this.inverseControl = !this.inverseControl;
        },
        /**
         * 供父组件使用，复位IndexControl
         * */
        resetIndexControl: function () {
          this.inverseControl = false;
        },
        /**
         * 供父组件使用，改变目前处于中心的图片相对应的小按钮的样式
         * @param centerIndex
         */
        changeCenter: function(centerIndex) {
          this.centerIndex = centerIndex;
        }
      }

    };
</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="less" rel="stylesheet/less" scoped>
  @import '../../common/less/style.less';
  @time: .8s;
  .bar{
    /*position: absolute;*/
    background-color: rgba(0,0,0,0.5);
    padding: .5rem 1.5rem .5rem 1.5rem;
    border-radius: 2rem;
    .unit{
      perspective: 1800px;
      transition: transform @time ease-in-out;
      display: inline-block;
      width: 2.5rem;
      height: 2.5rem;
      line-height: 2.5rem;
      border-radius: 50%;
      background-color: rgba(255,255,255,0.5);
      margin: 0 .5rem;
      color: darkgray;
      font-size: 1.5rem;
      text-align: center;
      cursor: pointer;
      .icon-spinner11:before {
        content: "\e984";
      }
      &.inverse{
        transform: rotateY(180deg);
      }
      &.centerFont{
        color: #ffffff;
      }
    }
  }
</style>
