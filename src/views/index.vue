<template>
    <div class="index" ref="index">
        <!-- 导航栏 -->
        <div class="nav">
            <div class="nav-list">
                <div :class="[curNum==index?'nav-item-cur nav-item':'nav-item']" v-for="(item,index) in tabList" :key="index" @click="tabTap(item.type,index)">
                  <span>{{item.text}}</span>
                </div>
            </div>
        </div>
        <!-- 照片列表 -->
        <div class="photo">
            <div class="box" v-for="(item,index) in imageList" :key="index" ref="box">
              <div class="pic">
                <img :src="item.src" alt="">
              </div>
            </div>
            
        </div>
    </div>
</template>

<style lang="less" scoped>
.index {
  min-height: 100vh;
  background-color: #f2f2f2;
  display: flex;
  flex-direction: row;
  .nav {
    width: 30%;
    position: fixed;
    left: 0;
    top: 0;
    min-height: 100vh;
    .nav-list {
      background-color: #fff;
      position: absolute;
      width: 100%;
      top: 0px;
      .nav-item {
        background-color: #f2f2f2;
        font-size: 0.4rem;
        padding: 0 0.25rem;
        height: 1rem;
        line-height: 1rem;
        span {
          display: block;
          width: 100%;
          // border-top: 1px solid rgba(7, 17, 27, 0.1);
        }
      }
      .nav-item-cur {
        background-color: #fff;
      }
    }
  }
  .photo {
    width: 70%;
    background-color: #fff;
    position: fixed;
    right: 0;
    top: 0;
    min-height: 100vh;
    overflow-y: scroll;
    .box {
      padding: 0.15rem;
      float: left;
      .pic {
        padding: 0.15rem;
        border: 1px solid #ccc;
        border-radius: 5px;
        box-shadow: 0 0 5px #ccc;
        img {
          width: 3rem;
          height: auto;
        }
      }
    }
  }
}
</style>

<script>
import Waterfall from "vue-waterfall/lib/waterfall";
import WaterfallSlot from "vue-waterfall/lib/waterfall-slot";

import vueWaterfallEasy from "vue-waterfall-easy";

export default {
  data () {
    return {
      tabList: [
        {
          text: "全部",
          type: "0"
        },
        {
          text: "晒单",
          type: "1"
        },
        {
          text: "海报",
          type: "2"
        },
        {
          text: "头像",
          type: "3"
        },
        {
          text: "商品",
          type: "4"
        }
      ],
      imageList: [
        {
          src: 'http://p0rz0hmjn.bkt.clouddn.com/about_02.jpg'
        },
        {
          src: 'http://p0rz0hmjn.bkt.clouddn.com/avatar.jpg'
        },
        {
          src: 'http://p0rz0hmjn.bkt.clouddn.com/banner_02.jpg'
        },
        {
          src: 'http://p0rz0hmjn.bkt.clouddn.com/card_lock.png'
        },
        {
          src: 'http://p0rz0hmjn.bkt.clouddn.com/conclusionabout_01.jpg'
        },
        {
          src: 'http://p0rz0hmjn.bkt.clouddn.com/fengyu.jpg'
        },
        {
          src: 'http://p0rz0hmjn.bkt.clouddn.com/lyyybg.jpg'
        },
        {
          src: 'http://p0rz0hmjn.bkt.clouddn.com/person.jpg'
        },
        {
          src: 'http://p0rz0hmjn.bkt.clouddn.com/personal_bg.jpg'
        },
        {
          src: 'http://p0rz0hmjn.bkt.clouddn.com/conclusionabout_01.jpg'
        },
        {
          src: 'http://p0rz0hmjn.bkt.clouddn.com/fengyu.jpg'
        },
        {
          src: 'http://p0rz0hmjn.bkt.clouddn.com/lyyybg.jpg'
        },
        {
          src: 'http://p0rz0hmjn.bkt.clouddn.com/person.jpg'
        },
        {
          src: 'http://p0rz0hmjn.bkt.clouddn.com/personal_bg.jpg'
        },
        {
          src: 'http://p0rz0hmjn.bkt.clouddn.com/xyhbban3.jpg'
        }
      ],
      fetchImgsArr: [],
      curNum: 0
    };
  },
  components: {
    Waterfall,
    WaterfallSlot,
    vueWaterfallEasy
  },
  methods: {
    // tab切换
    tabTap (type, index) {
      this.curNum = index;
    },

    initImg () {
      let boxs = this.$refs.box;
      console.log(boxs.length)

      // 计算整个页面显示的列数
      let boxW = boxs[0].offsetWidth;
      let windowW = this.$refs.index.offsetWidth * 0.7;
      let cols = Math.floor(windowW / boxW)
      console.log(cols)
      let hArr = [];
      for (let i = 0; i < boxs.length; i++) {
        if (i < cols) {
          hArr.push(boxs[i].offsetHeight)
        } else {
          let minH = Math.min.apply(null, hArr)
          let index = this.getMInIndex(hArr, minH)
          console.log(index)
          boxs[i].style.position = 'absolute';
          boxs[i].style.top = minH + 'px';
          boxs[i].style.left = boxW * index + 'px';
          hArr[index] += boxs[i].offsetHeight;

        }
      }
      console.log(hArr)

    },

    getMInIndex (arr, val) {
      for (const i in arr) {
        if (arr[i] == val) {
          return i

        }
      }
    }
  },

  mounted () {
    setTimeout(() => { this.initImg() }, 20)
  }
};
</script>