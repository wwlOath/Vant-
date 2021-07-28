<template>
  <div>
    <s-header :name="'全部'"></s-header>

    <div>
      <div class="search-wrap" ref="searchWrap">
        <div class="title"><b>为你推荐</b></div>
        <div ref="wrapper" class="app-list-wrapper">
          <list-scroll class="nav-side-wrapper" :width="contWidth">
            <ul class="cont" ref="cont">
              <li class="cont-item" v-for="item of categoryList" :key="item.id">
                <div class="cont-img">
                  <img class="img" :src="item.imgUrl" :alt="item.name">
                </div>
                <div class="cont-dest">{{item.name}}</div>
                <div class="cont-price">
                  <span class="price">￥{{item.categoryId}}</span>
                  <span>起</span>
                </div>
              </li>
            </ul>
          </list-scroll>
        </div>
        <van-row>
          <van-col span="5">
            <span class="title-attr"><b>我关注的</b></span>
          </van-col>
          <van-col span="19">
            <list-scroll class="nav-side-wrapper" :width="followWidth">
              <ul class="follow" ref="follow">
                <li class="follow-item-logo" v-for="item of categoryList" :key="item.id">
                  <div class="follow-img-logo">
                    <img class="img" :src="item.imgUrl" :alt="item.name">
                  </div>
                </li>
              </ul>
            </list-scroll>
          </van-col>
        </van-row>


      </div>
    </div>

    <div>
      <van-tabs v-model:active="active" :color="'#1baeae'" :title-active-color="'#1baeae'" offset-top="48px"  scrollspy sticky>
        <van-tab title="时尚穿搭">
          <div class="fashion">
            <div class="title"><b>时尚穿搭</b></div>
            <van-row type="flex" justify="space-between" v-for="item in categoryList" :key="item.categoryId">
              <van-col span="16">
                <van-row>
                  <van-col span="6">
                    <img :src="item.imgUrl">
                  </van-col>
                  <van-col span="18">
                    <div class="content">
                      <div><b>{{item.name}}</b></div>
                      <div class="desc">时尚穿搭{{item.name}}</div>
                    </div>
                  </van-col>
                </van-row>
              </van-col>
              <van-col span="6">
                <div style="text-align: right">
                  <van-button type="primary" round size="small"  icon="like-o">关注</van-button>
                </div>
              </van-col>
            </van-row>
          </div>
        </van-tab>
        <van-tab title="品质生活">
          <div class="fashion">
            <div class="title"><b>品质生活</b></div>
            <van-row type="flex" justify="space-between" v-for="item in categoryList" :key="item.categoryId">
              <van-col span="16">
                <van-row>
                  <van-col span="6">
                    <img :src="item.imgUrl">
                  </van-col>
                  <van-col span="18">
                    <div class="content">
                      <div><b>{{item.name}}</b></div>
                      <div class="desc">品质生活{{item.name}}</div>
                    </div>
                  </van-col>
                </van-row>

              </van-col>
              <van-col span="6">
                <div style="text-align: right">
                  <van-button type="primary" round size="small"  icon="like-o">关注</van-button>
                </div>
              </van-col>
            </van-row>
          </div>
        </van-tab>
        <van-tab title="优秀助手">
          <div class="fashion">
            <div class="title"><b>优秀助手</b></div>
            <van-row type="flex" justify="space-between" v-for="item in categoryList" :key="item.categoryId">
              <van-col span="16">
                <van-row>
                  <van-col span="6">
                    <img :src="item.imgUrl">
                  </van-col>
                  <van-col span="18">
                    <div class="content">
                      <div><b>{{item.name}}</b></div>
                      <div class="desc">优秀助手{{item.name}}</div>
                    </div>
                  </van-col>
                </van-row>

              </van-col>
              <van-col span="6">
                <div style="text-align: right">
                  <van-button type="primary" round size="small"  icon="like-o">关注</van-button>
                </div>
              </van-col>
            </van-row>
          </div>
        </van-tab>
        <van-tab title="特色频道">
          <div class="fashion">
            <div class="title"><b>特色频道</b></div>
            <van-row type="flex" justify="space-between" v-for="item in categoryList" :key="item.categoryId">
              <van-col span="16">
                <van-row>
                  <van-col span="6">
                    <img :src="item.imgUrl">
                  </van-col>
                  <van-col span="18">
                    <div class="content">
                      <div><b>{{item.name}}</b></div>
                      <div class="desc">特色频道{{item.name}}</div>
                    </div>
                  </van-col>
                </van-row>

              </van-col>
              <van-col span="6">
                <div style="text-align: right">
                  <van-button type="primary" round size="small"  icon="like-o">关注</van-button>
                </div>
              </van-col>
            </van-row>
          </div>
        </van-tab>
        <van-tab title="常用工具">
          <div class="fashion">
            <div class="title"><b>常用工具</b></div>
            <van-row type="flex" justify="space-between" v-for="item in categoryList" :key="item.categoryId">
              <van-col span="16">
                <van-row>
                  <van-col span="6">
                    <img :src="item.imgUrl">
                  </van-col>
                  <van-col span="18">
                    <div class="content">
                      <div><b>{{item.name}}</b></div>
                      <div class="desc">常用工具{{item.name}}</div>
                    </div>
                  </van-col>
                </van-row>

              </van-col>
              <van-col span="6">
                <div style="text-align: right">
                  <van-button type="primary" round size="small"  icon="like-o">关注</van-button>
                </div>
              </van-col>
            </van-row>
          </div>
        </van-tab>
      </van-tabs>
    </div>
  </div>
</template>

<style lang="less" scoped >
  @import '../common/style/mixin';
  .app-list-wrapper {
    width: 100%;
    .nav-side-wrapper {
      // scroll容器
      width: 100%;
      overflow: hidden;
    }
  }

  .title-attr {
    line-height: 70px;
    margin: 10px 15px;
  }

  .cont {
    list-style: none;
    white-space: nowrap;
    font-size: 12px;
    padding-right: .24rem;
    .cont-item {
      position: relative;
      display: inline-block;
      padding: .06rem 0 .2rem;
      width: 2rem;
      margin: 0 .1rem;
      text-align: center;
      .cont-img {
        overflow: hidden;
        width: 1rem;
        margin: 0 auto;
        .img {
          width: 100%;
        }
      }
      .cont-dest {
        margin: .1rem 0;
      }
      .cont-price {
        .price {
          color: #ff8300;
        }
      }
    }
  }
  .follow {
    list-style: none;
    white-space: nowrap;
    font-size: 12px;
    padding-right: .24rem;
    .follow-item-logo {
      position: relative;
      display: inline-block;
      padding: .06rem 0 .2rem;
      width: 1rem;
      margin: 0 .1rem;
      text-align: center;
      .follow-img-logo {
        overflow: hidden;
        width: 1rem;
        margin: 0 auto;
        .img {
          width: 100%;
        }
      }
    }
  }
  .search-wrap {
    .title {
      margin: 10px 15px;
    }
  }
  .van-button--small {
    height: 22px;
  }
  .fashion {
    padding: 0 15px;
    .title {
      margin: 10px 0;
    }
    img {
      .wh(36px, 36px);
      margin: 10px auto;
    }
    .content {
      margin: 10px auto;
      .desc {
        color: #969799;
        margin-top: 5px;
      }
    }
  }
</style>

<script>
  import sHeader from '@/components/SimpleHeader'
  import { reactive, toRefs, ref, onMounted } from 'vue'
  import listScroll from '@/components/horScroll'

  export default {
    setup() {
     const state = reactive({
       active: 0,
       categoryList: [
         {
           name: '新蜂超市',
           imgUrl: 'https://s.yezgea02.com/1604041127880/%E8%B6%85%E5%B8%82%402x.png',
           categoryId: 100001
         }, {
           name: '新蜂服饰',
           imgUrl: 'https://s.yezgea02.com/1604041127880/%E6%9C%8D%E9%A5%B0%402x.png',
           categoryId: 100003
         }, {
           name: '全球购',
           imgUrl: 'https://s.yezgea02.com/1604041127880/%E5%85%A8%E7%90%83%E8%B4%AD%402x.png',
           categoryId: 100002
         }, {
           name: '新蜂生鲜',
           imgUrl: 'https://s.yezgea02.com/1604041127880/%E7%94%9F%E9%B2%9C%402x.png',
           categoryId: 100004
         }, {
           name: '新蜂到家',
           imgUrl: 'https://s.yezgea02.com/1604041127880/%E5%88%B0%E5%AE%B6%402x.png',
           categoryId: 100005
         }, {
           name: '充值缴费',
           imgUrl: 'https://s.yezgea02.com/1604041127880/%E5%85%85%E5%80%BC%402x.png',
           categoryId: 100006
         }, {
           name: '9.9元拼',
           imgUrl: 'https://s.yezgea02.com/1604041127880/9.9%402x.png',
           categoryId: 100007
         }, {
           name: '领劵',
           imgUrl: 'https://s.yezgea02.com/1604041127880/%E9%A2%86%E5%88%B8%402x.png',
           categoryId: 100008
         }, {
           name: '省钱',
           imgUrl: 'https://s.yezgea02.com/1604041127880/%E7%9C%81%E9%92%B1%402x.png',
           categoryId: 100009
         }, {
           name: '全部',
           imgUrl: 'https://s.yezgea02.com/1604041127880/%E5%85%A8%E9%83%A8%402x.png',
           categoryId: 100010
         },
       ],
       contWidth: '',
       followWidth: ''
     });

      const cont = ref(null);
      const follow = ref(null);

      onMounted(async () => {
        let contWidth = document.getElementsByClassName('cont')[0].scrollWidth;
        let followWidth = document.getElementsByClassName('follow')[0].scrollWidth;

        state.contWidth = contWidth + 20;
        state.followWidth = followWidth + 20;
      })

     return {
       ...toRefs(state),
       cont,
       follow
     }
    },
    components: {
      sHeader,
      listScroll
    },
  }

</script>