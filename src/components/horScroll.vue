<template>
  <div class="recommand-wrap">
    <div ref="wrapper">
      <div ref="cont">
        <slot></slot>
      </div>
    </div>
  </div>
</template>

<script>
  import BScroll from 'better-scroll'

  export default {
    name: 'horScroll',
    props: {
      width: {
        type: Number,
        required: true
      }
    },
    components: {

    },
    data () {
      return {

      }
    },
    methods: {
      verScroll () {
        this.$refs.cont.style.width = this.width + 'px'  // 修改滚动区域的宽度
        this.$nextTick(() => {
          if (!this.scroll) {
            this.scroll = new BScroll(this.$refs.wrapper, {
              startX: 0,  // 配置的详细信息请参考better-scroll的官方文档，这里不再赘述
              click: true,
              scrollX: true,
              scrollY: false,
              eventPassthrough: 'vertical'
            })
          } else {
            this.scroll.refresh() //如果dom结构发生改变调用该方法
          }
        })
      }
    },
    mounted () {
      this.$nextTick(() => {
        let timer = setTimeout(() => { // 其实我也不想写这个定时器的，这相当于又嵌套了一层$nextTick，但是不这么写会失败
          if (timer) {
            clearTimeout(timer)
            this.verScroll()
          }
        }, 0)
      })
    }
  }
</script>

<style lang="less" scoped>
  .recommand-wrap {
    margin-top: .2rem;
    background: #fff;
    width: 100%;
    touch-action: pan-y;
    overflow: hidden;
  }
</style>