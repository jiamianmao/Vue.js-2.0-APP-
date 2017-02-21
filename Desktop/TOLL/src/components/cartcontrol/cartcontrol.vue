<template>
  <div class="cartcontrol">
    <transition name="fade">
        <div class="cart-decrease" v-show="food.count>0" @click.stop.prevent="decreaseCart($event)">
          <transition name="inner">
            <span class="inner icon-remove_circle_outline"></span>
          </transition>
        </div>
    </transition>
    <div class="cart-count" v-show="food.count > 0 ">{{food.count}}</div>
    <div class="cart-add iconfont icon-add_circle" @click.stop.prevent="addCart($event)"></div>
  </div>
</template>

<script type="text/ecmascript-6">
  import Vue from 'vue';

  export default {
    props: {
      food: {
        type: Object
      }
    },
    methods: {
      addCart (event) {
        if (!event._constructed) {
          // 去掉自带click事件的点击
          return;
        }
        if (!this.food.count) {
          Vue.set(this.food, 'count', 1);
        } else {
          this.food.count++;
        }
//        event.srcElement.outerHTML
        this.$emit('increment', event.target); // 子组件通过 $emit触发父组件的方法 increment   还
      },
      decreaseCart (event) {
        if (!event._constructed) {
          // 去掉自带click事件的点击
          return;
        }
        this.food.count--;
      }
    }
  };
</script>
<style lang="stylus" rel="stylesheet/stylus">
  @import "cartControl.styl";
</style>