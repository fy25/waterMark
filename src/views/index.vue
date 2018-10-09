<template>
    <div class="index">
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
            <vue-waterfall-easy :imgsArr="imgsArr" @scrollLoadImg="fetchImgsData"></vue-waterfall-easy>
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
    position: relative;
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
    img {
      width: 100%;
    }
  }
}
</style>

<script>
import Waterfall from "vue-waterfall/lib/waterfall";
import WaterfallSlot from "vue-waterfall/lib/waterfall-slot";

import vueWaterfallEasy from "vue-waterfall-easy";

export default {
  data() {
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
      imgsArr: [
        {
          src: "http://p0rz0hmjn.bkt.clouddn.com/about_02.jpg",
          link: "",
          info: "一些图片描述文字"
        },
        {
          src: "http://p0rz0hmjn.bkt.clouddn.com/xyhbban1.jpg",
          link: "",
          info: "一些图片描述文字"
        },
        {
          src: "http://p0rz0hmjn.bkt.clouddn.com/about_02.jpg",
          link: "",
          info: "一些图片描述文字"
        },
        {
          src: "http://p0rz0hmjn.bkt.clouddn.com/xyhbban1.jpg",
          link: "",
          info: "一些图片描述文字"
        },
        {
          src: "http://p0rz0hmjn.bkt.clouddn.com/about_02.jpg",
          link: "",
          info: "一些图片描述文字"
        },
        {
          src: "http://p0rz0hmjn.bkt.clouddn.com/xyhbban1.jpg",
          link: "",
          info: "一些图片描述文字"
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
  mounted() {},
  methods: {
    initImgsArr(n, m) {
      //初始化图片数组的方法，把要加载的图片装入
      var arr = [];
      for (var i = n; i < m; i++) {
        arr.push({
          src: "http://p0rz0hmjn.bkt.clouddn.com/about_02.jpg",
          link: "",
          info: "一些图片描述文字"
        }); //src为加载的图片的地址、link为超链接的链接地址、 //info为自定义的图片展示信息，请根据自己的情况自行填写
      }
      return arr;
    },

    fetchImgsData() {
      //获取新的图片数据的方法，用于页面滚动满足条件时调用
      this.imgsArr = this.imgsArr.concat(this.fetchImgsArr); //数组拼接，把下一批要加载的图片放入所有图片的数组中
    },

    // tab切换
    tabTap(type, index) {
      this.curNum = index;
    }
  },

  created() {
    // this.imgsArr = this.initImgsArr(0, 10);
  }
};
</script>