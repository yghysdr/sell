<template>
  <div class="card">
    <div class="left-wrapper">
      <div class="logo-wrapper">
        <div class="logo">
          <i class="icon-shopping_cart"></i>
        </div>
        <div class="num" v-show="totalCount>0">{{totalCount}}</div>
      </div>
      <div class="price">￥{{totalPrice}}</div>
      <div class="desc">另需配送费￥{{deliveryPrice}}元</div>
    </div>
    <div class="right-wrapper" :class="payClass">
      <span class="pay">{{payDesc}}</span>
    </div>

  </div>
</template>

<script type="text/ecmascript-6">
  export default {
    props: {
      'selectFoods': {
        type: Array,
        default () {
          return [
            {
              price: 11,
              count: 1
            }
          ];
        }
      },
      'deliveryPrice': {
        type: Number,
        default: 10
      },
      'minTotalPrice': {
        type: Number,
        default: 15
      }
    },
    computed: {
      totalPrice () {
        let total = 0;
        this.selectFoods.forEach((food) => {
          total = food.count * food.price;
        });
        return total;
      },
      totalCount () {
        let count = 0;
        this.selectFoods.forEach((food) => {
          count += food.count;
        });
        console.log(count);
        return count;
      },
      payDesc () {
        if (this.totalPrice === 0) {
          return `￥${this.minTotalPrice}元起送`;
        } else if (this.totalPrice < this.minTotalPrice) {
          let diff = this.minTotalPrice - this.totalPrice;
          return `还差￥${diff}元起送`;
        } else {
          return '去结算';
        }
      },
      payClass () {
        if (this.totalPrice < this.minTotalPrice) {
          return 'nu-enough';
        } else {
          return 'enough';
        }
      }
    }
  };
</script>

<style lang="stylus" rel="stylesheet/stylus">
  @import "../../common/stylus/mixin.styl"

  .card
    display: flex
    width: 100%
    height: 48px
    background: #141d27
    color: rgba(255, 255, 255, 0.4)
    font-size: 0
    .left-wrapper
      flex: 1
      .logo-wrapper
        display: inline-block
        position: relative
        top: -10px
        margin: 0px 12px
        width: 56px
        height: 56px
        border-radius: 50%
        background: #141d27
        padding: 6px
        .logo
          width: 100%
          height: 100%
          border-radius: 50%
          text-align: center
          background: #2b343c
          .icon-shopping_cart
            line-height: 44px
            font-size: 24px
            color: #80858a
        .num
          position: absolute
          top: 0
          right: 0
          min-width: 24px
          padding: 0px 3px
          height: 16px
          line-height: 16px
          text-align: center
          border-radius: 16px
          font-size: 9px
          font-weight: 700
          color: #fff
          background: rgb(240, 20, 20)
          box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.4)
      .price
        display: inline-block
        vertical-align: top
        margin-top: 12px
        line-height: 24px
        border-right: 1px solid rgba(255, 255, 255, 0.1)
        padding-right: 12px
        font-size: 16px
        font-weight: 700
      .desc
        display: inline-block
        vertical-align: top
        margin-top: 12px
        line-height: 24px
        padding-left: 12px
        font-size: 10px
    .right-wrapper
      display: flex
      align-items: center
      justify-content: center
      width: 105px
      flex: 0 0 105px
      &.enough
        background: #00b43c
        color: #fff
      &.nu-enough
        background: #2b333b
      .pay
        line-height 24px
        font-size: 12px
        font-weight 700px


</style>