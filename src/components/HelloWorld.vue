<template>
  <div
    style="
      width: 100vw;
      height: 100vh;
      background-color: #000000;
      overflow: auto;
      text-align: center;
      color: #666;
    "
  >
    <audio
      style="margin: 30px auto; width: 420px"
      controls
      src="../assets/难念的经  - 周华健.mp3"
    ></audio>
    <div class="container">
      <ul></ul>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      indexPars: null,
      clientHeight: null,
      maxOffset: null,
      liHeight: null,
      dome: {},
      result: [],
      lrc: `[00:01.06]难念的经
[00:03.95]演唱：周华健
[00:06.78]
[00:30.96]笑你我枉花光心计
[00:34.15]爱竞逐镜花那美丽
[00:36.75]怕幸运会转眼远逝
[00:39.32]为贪嗔喜恶怒着迷
[00:41.99]责你我太贪功恋势
[00:44.48]怪大地众生太美丽
[00:47.00]悔旧日太执信约誓
[00:49.66]为悲欢哀怨妒着迷
[00:52.56]啊 舍不得璀灿俗世
[00:57.66]啊 躲不开痴恋的欣慰
[01:02.86]啊 找不到色相代替
[01:08.09]啊 参一生参不透这条难题
[01:13.15]吞风吻雨葬落日未曾彷徨
[01:15.73]欺山赶海践雪径也未绝望
[01:18.23]拈花把酒偏折煞世人情狂
[01:20.90]凭这两眼与百臂或千手不能防
[01:23.76]天阔阔雪漫漫共谁同航
[01:26.09]这沙滚滚水皱皱笑着浪荡
[01:28.68]贪欢一刻偏教那女儿情长埋葬
[01:32.38]
[01:34.09]吞风吻雨葬落日未曾彷徨
[01:36.50]欺山赶海践雪径也未绝望
[01:39.07]拈花把酒偏折煞世人情狂
[01:41.69]凭这两眼与百臂或千手不能防
[01:44.68]天阔阔雪漫漫共谁同航
[01:46.93]这沙滚滚水皱皱笑着浪荡
[01:49.54]贪欢一刻偏教那女儿情长埋葬
[01:53.41]
[02:15.45]笑你我枉花光心计
[02:18.53]爱竞逐镜花那美丽
[02:21.14]怕幸运会转眼远逝
[02:23.76]为贪嗔喜恶怒着迷
[02:26.43]责你我太贪功恋势
[02:28.98]怪大地众生太美丽
[02:31.60]悔旧日太执信约誓
[02:34.26]为悲欢哀怨妒着迷
[02:36.90]啊 舍不得璀灿俗世
[02:42.04]啊 躲不开痴恋的欣慰
[02:47.34]啊 找不到色相代替
[02:52.52]啊 参一生参不透这条难题
[02:57.47]吞风吻雨葬落日未曾彷徨
[03:00.05]欺山赶海践雪径也未绝望
[03:02.64]拈花把酒偏折煞世人情狂
[03:05.27]凭这两眼与百臂或千手不能防
[03:08.22]天阔阔雪漫漫共谁同航
[03:10.49]这沙滚滚水皱皱笑着浪荡
[03:13.06]贪欢一刻偏教那女儿情长埋葬
[03:18.45]吞风吻雨葬落日未曾彷徨
[03:20.90]欺山赶海践雪径也未绝望
[03:23.54]拈花把酒偏折煞世人情狂
[03:26.21]凭这两眼与百臂或千手不能防
[03:29.07]天阔阔雪漫漫共谁同航
[03:31.32]这沙滚滚水皱皱笑着浪荡
[03:33.92]贪欢一刻偏教那女儿情长埋葬
[03:39.32]吞风吻雨葬落日未曾彷徨
[03:41.84]欺山赶海践雪径也未绝望
[03:44.38]拈花把酒偏折煞世人情狂
[03:47.04]凭这两眼与百臂或千手不能防
[03:49.99]天阔阔雪漫漫共谁同航
[03:52.20]这沙滚滚水皱皱笑着浪荡
[03:54.89]贪欢一刻偏教那女儿情长埋葬
[04:00.28]吞风吻雨葬落日未曾彷徨
[04:02.68]欺山赶海践雪径也未绝望
[04:05.25]拈花把酒偏折煞世人情狂
[04:07.90]凭这两眼与百臂或千手不能防
[04:10.85]天阔阔雪漫漫共谁同航
[04:13.08]这沙滚滚水皱皱笑着浪荡
[04:15.75]贪欢一刻偏教那女儿情长埋葬
[04:19.48]END`,
    };
  },
  mounted() {
    //先处理歌词，变成数组形式，便于操作
    let listMusic = this.lrc.split("\n");
    // let result = []
    // for(let i=0;i<listMusic.length;i++){
    //     let str = res
    //     let parts = ste.split(']')
    //     let  timeStr = parts[0].substring(1);
    //     let obj={
    //         timef:partsTime(timeStr),
    //         words:parts(1)
    //     }
    //     result .push(obj)
    // }
    /**
     * 把时间变成秒
     * 数组形式
     * result[{time:'播放的时间',words:'歌词' }]
     */
    listMusic.map((res) => {
      let str = res;
      let parts = str.split("]");
      let timeStr = parts[0].substring(1);
      let obj = {
        time: this.partsTime(timeStr),
        words: parts[1],
      };
      this.result.push(obj);
    });
    this.dome = {
      audio: document.querySelector("audio"),
      ul: document.querySelector(".container ul"),
      contain: document.querySelector(".container"),
    };
    this.createDataElements();

    this.dome.audio.addEventListener("timeupdate", this.setOffset);
  },
  methods: {
    /**
     * 创建歌词元素 li
     */
    createDataElements() {
      let frag = document.createDocumentFragment(); //文档片段
      for (let i = 0; i < this.result.length; i++) {
        let li = document.createElement("li");
        //创建li标签
        li.textContent = this.result[i].words;
        // //加入到我们页面里ul标签里面去 这里牵扯到效率问题（当然这里可以忽略不计）
        // this.dome.ul.appendChild(li);
        frag.appendChild(li);
        this.dome.ul.appendChild(frag);
      }
      this.clientHeight = this.dome.contain.clientHeight; //获取contain的高度
      this.liHeight = this.dome.ul.children[0].clientHeight; //获取lio标签的高度
      this.maxOffset = this.dome.ul.clientHeight - this.clientHeight; //最大值的时候
    },

    /**
     * 将时间字符串解析成数字（秒）
     * @param timeStr
     * @returns {number}
     */
    partsTime(timeStr) {
      let parts = timeStr.split(":");
      return +parts[0] * 60 + +parts[1];
    },
    /**
     * 计算出当前播放器播放到第几秒的情况下
     * 数组中歌词那一句应该高亮显示（取下标）
     *若没有任何依据歌词要显示则返回-1
     */
    findInde() {
      let timfes = this.dome.audio.currentTime;
      for (let i = 0; i < this.result.length; i++) {
        if (timfes < this.result[i].time) {
          return i - 1;
        }
      }
      //歌词到了最后所显示的下标
      return this.result.length - 1;
    },
    /**
     * 设置ul的的偏移量
     */
    setOffset() {
      let index = Number(this.findInde());
      let offset =
        this.liHeight * index + this.liHeight / 2 - this.clientHeight / 2;
      //注意刚开始的时候相减为负和最大值的时候数所以要做边界判断
      //刚开始播放的时候的边界
      if (offset < 0) {
        offset = 0;
      }
      //播放完了之后的边界
      if (offset > this.maxOffset) {
        offset = this.maxOffset;
      }
      //偏移
      this.dome.ul.style.transform = `translateY(-${offset}px)`;

      //重置li标签样式
      let li = this.dome.ul.querySelector(".active");
      if (li) {
        li.classList.remove("active");
      }
      //高亮显示
      // this.dome.children[index].className="active" //第一种
      // this.dome.children[index].classList.add("active")//第二种
      //刚播放的时候计算出来的值为负数所以没有标签得判断一下
      li = this.dome.ul.children[index];
      if (li) {
        li.classList.add("active");
      }
    },
  },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
}
.container {
  height: 420px;
  overflow: hidden;
}
.container ul {
  list-style: none;
  transition: 0.6s;
}
.container li {
  height: 30px;
  line-height: 30px;
  transition: 0.2s;
}
.container li.active {
  color: #fff;
  transform: scale(1.2);
}
</style>
