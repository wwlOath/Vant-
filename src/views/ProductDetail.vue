<!--
 * 严肃声明：
 * 开源版本请务必保留此注释头信息，若删除我方将保留所有法律责任追究！
 * 本系统已申请软件著作权，受国家版权局知识产权以及国家计算机软件著作权保护！
 * 可正常分享和学习源码，不得用于违法犯罪活动，违者必究！
 * Copyright (c) 2020 陈尼克 all rights reserved.
 * 版权所有，侵权必究！
 *
-->

<template>
  <div class="product-detail">
    <s-header :name="'商品详情'"></s-header>
    <div class="detail-content" @scroll="handleScroll">
      <div class="detail-swipe-wrap">
        <van-swipe class="my-swipe" indicator-color="#1baeae">
          <van-swipe-item v-for="(item, index) in detail.goodsCarouselList" :key="index">
            <img :src="item" alt="">
          </van-swipe-item>
        </van-swipe>
      </div>
      <div class="product-info">
        <div class="product-title">
          {{ detail.goodsName || '' }}
        </div>
        <div class="product-desc">免邮费 顺丰快递</div>
        <div class="product-price">
          <span>¥{{ detail.sellingPrice || '' }}</span>
          <!-- <span>库存203</span> -->
        </div>
      </div>
      <div class="product-intro">
        <van-tabs :color="'#1baeae'" :title-active-color="'#1baeae'">
          <van-tab title="概述">
            <div class="product-content" v-html="detail.goodsDetailContent || ''"></div>
          </van-tab>
          <van-tab title="规则与包装">
            <van-divider>包装清单</van-divider>
            <div style="padding-left: 20px;">主机 x1，数据线 x1，充电器 x1，SIM卡通针x1，保护套x1，快速入门指南x1，重要信息指南（含保修卡）x1</div>
            <van-divider>商品参数</van-divider>
            <van-cell-group inset>
              <van-cell title="商品编号" value="100020269344" />
              <van-cell title="后置摄像头"/>
              <van-cell title="后摄主摄光圈" value="f/1.7"/>
              <van-cell title="后摄主摄光学防抖" value="不支持光学防抖"/>
              <van-cell title="闪光灯" value="其他闪光灯"/>
              <van-cell title="操作系统"/>
              <van-cell title="操作系统版本" value="ColorOS"/>
              <van-cell title="前置摄像头"/>
              <van-cell title="前摄主摄光圈" value="f/2.0"/>
              <van-cell title="辅助功能"/>
              <van-cell title="常用功能" value="便签；计算器；录音；重力感应"/>
              <van-cell title="手机特性"/>
              <van-cell title="三防标准" value="不支持防水"/>
            </van-cell-group>
          </van-tab>
          <van-tab title="售后保障">
            <div style="padding: 0 15px;">
              <p>本商品质保周期为1年质保，在此时间范围内可提交维修申请，具体以厂家服务为准。</p>
              <p>如因质量问题或故障，凭厂商维修中心或特约维修点的质量检测证明，享受7日内退货，15日内换货，15日以上在质保期内享受免费保修等三包服务！</p>
              <p>注： 如厂家在商品介绍中有售后保障的说明，则此商品按照厂家说明执行售后保障服务。您可以查询本品牌在各地售后服务中心的联系方式，<a href="">请点击这儿查询...</a></p>
              <van-divider>服务承诺</van-divider>
              <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Assumenda dolorem, facere fugiat illo in ipsa nihil, optio perspiciatis quia rerum, tenetur ut voluptate! Aspernatur, cupiditate eum ex ipsam quam quod.</p>
              <van-divider>权利声明</van-divider>
              <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Ad adipisci dicta dignissimos dolor enim explicabo id, libero numquam quae, quam ratione reprehenderit sunt veritatis vero, voluptas. Debitis rem sunt vero.</p>
              <van-divider>价格说明</van-divider>
              <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Animi aperiam assumenda, beatae commodi dignissimos eius iure libero optio quae quia temporibus totam. Commodi debitis dolorum itaque quo voluptate. Dignissimos, pariatur!</p>
            </div>
          </van-tab>
        </van-tabs>

      </div>
    </div>
    <van-action-bar>
      <van-action-bar-icon icon="chat-o" text="客服" />
      <van-action-bar-icon icon="cart-o" :badge="!count ? '' : count" @click="goTo()" text="购物车" />
      <van-action-bar-button type="warning" @click="handleAddCart" text="加入购物车" />
      <van-action-bar-button type="danger" @click="goToCart" text="立即购买" />
    </van-action-bar>

    <van-button type="primary" size="small" square class="backTop" @click="backTop" v-show="flag_scroll">
      <van-icon name="arrow-up" />
    </van-button>
  </div>
</template>

<script>
import { reactive, onMounted, computed, toRefs, nextTick } from 'vue'
import { useRoute, useRouter } from 'vue-router'
import { useStore } from 'vuex'
import { getDetail } from '@/service/good'
import { addCart } from '@/service/cart'
import sHeader from '@/components/SimpleHeader'
import { Toast } from 'vant'
import { prefix } from '@/common/js/utils'
export default {
  setup() {
    const route = useRoute()
    const router = useRouter()
    const store = useStore()

    const state = reactive({
      detail: {
        goodsCarouselList: []
      },
      flag_scroll: false
    })

    onMounted(async () => {
      const { id } = route.params
      const { data } = await getDetail(id)
      data.goodsCarouselList = data.goodsCarouselList.map(i => prefix(i))
      state.detail = data
      store.dispatch('updateCart')
    })

    nextTick(() => {
      // 一些和DOM有关的东西
      const content = document.querySelector('.detail-content')
      content.scrollTop = 0
    })

    const handleScroll = () => {
      let scrollTop = document.getElementsByClassName('detail-content')[0].scrollTop;

      if(scrollTop > 100){
        state.flag_scroll = true
      }else {
        state.flag_scroll = false
      }
    };

    const backTop = () => {
      let top = document.getElementsByClassName('detail-content')[0].scrollTop;
      const timeTop = setInterval(() => {
        document.getElementsByClassName('detail-content')[0].scrollTop = document.getElementsByClassName('detail-content')[0].scrollTop = top -= 50
        if (top <= 0) {
          clearInterval(timeTop)
        }
      }, 10)
    };

    const goBack = () => {
      router.go(-1)
    }

    const goTo = () => {
      router.push({ path: '/cart' })
    }

    const handleAddCart = async () => {
      const { resultCode } = await addCart({ goodsCount: 1, goodsId: state.detail.goodsId })
      if (resultCode == 200 ) Toast.success('添加成功')
      store.dispatch('updateCart')
    }

    const goToCart = async () => {
      await addCart({ goodsCount: 1, goodsId: state.detail.goodsId })
      store.dispatch('updateCart')
      router.push({ path: '/cart' })
    }

    const count = computed(() => {
      return store.state.cartCount
    })

    return {
      ...toRefs(state),
      goBack,
      goTo,
      handleAddCart,
      goToCart,
      count,
      backTop,
      handleScroll
    }
  },
  components: {
    sHeader
  }
}
</script>

<style lang="less">
  @import '../common/style/mixin';
  .product-detail {
    .backTop {
      position: fixed;
      bottom: 60px;
      right: 5px;
    }
    .detail-header {
      position: fixed;
      top: 0;
      left: 0;
      z-index: 10000;
      .fj();
      .wh(100%, 44px);
      line-height: 44px;
      padding: 0 10px;
      .boxSizing();
      color: #252525;
      background: #fff;
      border-bottom: 1px solid #dcdcdc;
      .product-name {
        font-size: 14px;
      }
    }
    .detail-content {
      height: calc(100vh - 50px);
      overflow: hidden;
      overflow-y: auto;
      .detail-swipe-wrap {
        .my-swipe .van-swipe-item {
          img {
            width: 100%;
            // height: 300px;
          }
        }
      }
      .product-info {
        padding: 0 10px;
        .product-title {
          font-size: 14px;
          font-weight: bold;
          text-align: left;
          color: #333;
        }
        .product-desc {
          font-size: 12px;
          text-align: left;
          color: #999;
          padding: 5px 0;
        }
        .product-price {
          .fj();
          span:nth-child(1) {
            color: #F63515;
            font-size: 20px;
            margin-top: 5px;
          }
          span:nth-child(2) {
            color: #999;
            font-size: 16px;
          }
        }
      }
      .product-intro {
        width: 100%;
        padding-bottom: 50px;
        .van-cell {
          font-size: 10px;
        }
        ul {
          .fj();
          width: 100%;
          margin: 10px 0;
          li {
            flex: 1;
            padding: 5px 0;
            text-align: center;
            font-size: 15px;
            border-right: 1px solid #999;
            box-sizing: border-box;
            &:last-child {
              border-right: none;
            }
          }
        }
        .product-content {
          padding: 0 20px;
          img {
            width: 100%;
          }
        }
      }
    }
    .van-action-bar-button--warning {
      background: linear-gradient(to right,#6bd8d8, @primary)
    }
    .van-action-bar-button--danger {
      background: linear-gradient(to right, #0dc3c3, #098888)
    }
  }
</style>
