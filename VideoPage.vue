<template>
  <div class="video_box_content">

    <!--头部视频部分-->
    <div class="video_head_image">
      <video src="http://vali.cp31.ott.cibntv.net/youku/6573eccc484357154b415535a/03000801005B4ED99C4C14131CB6846FC9F460-3DC3-FF25-EC1A-996DD4C9EDB9.mp4?sid=054580823500010002783_00_A5f13ac20f271a8be99aecc0eb3bf39aa&sign=64d349a6ce21124777c6a967930cb96d&ctype=50"></video>
    </div>

    <div class="video_all_hidden" v-if="expandedDom">
      <!--视频标签介绍-->
      <div class="video_tab">

        <!--标签按钮-->
        <div class="video_tab_btn">
          <p class="video_tab_p" v-for="(val,i) in swipeTabList" @click="changeSwipeItemIndex(i)">{{val}}</p>
        </div>

        <!--标签对应的tab页面-->
        <div class="video_tab_content">
          <swiper :aspect-ratio="300/800" style="height: 500px;" @on-index-change="onSwipeItemIndexChange" v-model="swipeItemIndex" :show-dots="false">
            <swiper-item class="swiper-demo-img" v-for="(item, index) in swipeList" :key="index">
              <div class="video_swipe_content">
                故事发生在非洲附近的大海上，主人公冷锋遭遇人生滑铁卢,被“开除军籍”，本想漂泊一生的他，正当他打算这么做的时候，一场突如其来的意外打破了主人公冷锋全部的计划
                <!--控制video_tab_content 高度实现隐藏与显示-->
                <div class="video_swipe_show" @click="selectSwipe(index)" v-if="!showSwipeBtn[index]">展开全部</div>
                <div class="video_swipe_show" @click="selectSwipe(index)" v-if="showSwipeBtn[index]">关闭全部</div>
              </div>
            </swiper-item>
          </swiper>
        </div>
      </div>

      <!--基础信息-->
      <div class="video_baseInformation">
        <div class="detail_body_information_title remove_padding">
          <p class="detail_border_left"></p>
          <p class="detail_border_content">基础信息</p>
        </div>
        <div class="video_baseInformation_tab">
          <p class="video_tab_second" v-for="(val,index) in swipeTagArr" @click="changAddClass(index)">{{val}}</p>
        </div>
      </div>

      <!--进度条部分-->
      <div class="detail_body_lineBar">
        <div class="video_lineBar_content" v-if="informationNumber.length > 0" v-for="(val,index) in informationNumber">
            <div class="video_lineBar_name">{{val.name}}:</div>
            <div class="video_lineBar_number">{{val.number}}</div>
            <div class="video_lineBar_barShow">
              <div class="video_lineBar_barShow_cover" :style="'width:' + val.len + 'rem'"></div>
            </div>
            <div class="video_lineBar_info">{{val.info}}</div>
          </div>
      </div>

      <!--视频列表-->
      <div class="video_select_list">
        <div class="detail_body_information_title remove_padding">
          <p class="detail_border_left"></p>
          <p class="detail_border_content">视频列表</p>
        </div>
        <div class="select_video_list">
          <div class="select_list_first" :class="i > 2 ? 'select_list_first_add':''" v-for="(val,i) in videoList" @click="openApp">
            <div class="select_img_box">
              <img :src="val['imgUrl']" alt="图片损坏">
            </div>
            <div class="select_img_name">{{val['name']}}</div>
          </div>
        </div>
      </div>
    </div>

    <!--展开按钮-->
    <div class="concat_dom" @click="showHideDom" v-if="!expandedDom">
      <div class="concat_icon"></div>
      <div class="concat_name">展开</div>
    </div>

    <!--精彩内容-->
    <div class="detail_splendid_content">
      <div class="detail_body_information_title remove_padding">
        <p class="detail_border_left"></p>
        <p class="detail_border_content">精选内容</p>
      </div>
      <div class="detail_down_btn_box">
        <div class="detail_down_btn" @click="openApp">打开潘多拉查看全部</div>
      </div>
    </div>

    <!--神奇世界页面最后一部分-->
    <div class="video_magical_word">
      <div class="detail_body_information_title remove_padding">
        <p class="detail_border_left"></p>
        <p class="detail_border_content">神奇世界</p>
      </div>
      <div class="video_magical_box">
        <div :class="[ index == magicWord.length -1 ? 'video_magical_list video_magical_list_end':'video_magical_list']" v-for="(item,index) in magicWord">
          <div class="video_magical_content">
            <div class="video_magical_content_left">
              <div class="magical_word">{{item.wordTitle}}</div>
              <div class="magical_open_app" @click="openApp">打开App</div>
            </div>
            <div class="video_magical_content_right">
              <img :src="item.imgUrl" alt="">
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { Swiper, SwiperItem } from 'vux'
export default {
  name: "VideoPage",
  components:{
    Swiper,
    SwiperItem,
  },
  data() {
    return {
      swipeList: [
        'http://placeholder.qiniudn.com/800x300/FF3B3B/ffffff',
        'http://placeholder.qiniudn.com/800x300/FFEF7D/ffffff',
        'http://placeholder.qiniudn.com/800x300/8AEEB1/ffffff'
      ],
      swipeItemIndex: 0,
      showSwipeBtn: [],
      swipeTabList: ['导演','演员','导演2'],
      swipeTagArr: ['男','香港','新界','香港','新界','香港','新界','香港','新界','香港','新界'],
      magicWord: [
        {
          wordTitle: "史上最长乐曲演奏完要639年敢问还有比这更久的吗？",
          imgUrl:"https://ss3.baidu.com/-fo3dSag_xI4khGko9WTAnF6hhy/image/h%3D300/sign=6f4318466e2762d09f3ea2bf90ed0849/5243fbf2b211931376d158d568380cd790238dc1.jpg"
        },
        {
          wordTitle: "公司不允许员工有秘密，谈恋爱不汇报罚做50次下蹲运动。",
          imgUrl:"https://ss3.baidu.com/-fo3dSag_xI4khGko9WTAnF6hhy/image/h%3D300/sign=6f4318466e2762d09f3ea2bf90ed0849/5243fbf2b211931376d158d568380cd790238dc1.jpg"
        },
        {
          wordTitle: "重庆两车相撞堵塞机场路，千人携行李跑步赶飞机",
          imgUrl:"https://ss3.baidu.com/-fo3dSag_xI4khGko9WTAnF6hhy/image/h%3D300/sign=6f4318466e2762d09f3ea2bf90ed0849/5243fbf2b211931376d158d568380cd790238dc1.jpg"
        },
        {
          wordTitle: "司老板情人节留人加班工资翻倍，除经理外无人留下",
          imgUrl:"https://ss3.baidu.com/-fo3dSag_xI4khGko9WTAnF6hhy/image/h%3D300/sign=6f4318466e2762d09f3ea2bf90ed0849/5243fbf2b211931376d158d568380cd790238dc1.jpg"
        },
        {
          wordTitle: "对父母卖掉家产，在儿子失明前伴其游世界",
          imgUrl:"https://ss3.baidu.com/-fo3dSag_xI4khGko9WTAnF6hhy/image/h%3D300/sign=6f4318466e2762d09f3ea2bf90ed0849/5243fbf2b211931376d158d568380cd790238dc1.jpg"
        }
      ],//存储神奇世界中的数据,
      informationNumber: [
        {
          'name': '成龙',
          'number': '10',
          'len': 0.6,
          'info': '成龙电影'
        },
        {
          'name': '成龙',
          'number': '10',
          'len': 0.6,
          'info': '成龙电影'
        }
      ],
      videoList: [
        {
          imgUrl: 'https://desk-fd.zol-img.com.cn/t_s960x600c5/g5/M00/03/01/ChMkJlv88omIdK2ZAA1NpydpvQoAAtamwNQaEgADU2_018.jpg',
          name: '1'
        },
        {
          imgUrl: 'https://desk-fd.zol-img.com.cn/t_s960x600c5/g5/M00/03/01/ChMkJlv88omIdK2ZAA1NpydpvQoAAtamwNQaEgADU2_018.jpg',
          name: '2'
        },
        {
          imgUrl: 'https://desk-fd.zol-img.com.cn/t_s960x600c5/g5/M00/03/01/ChMkJlv88omIdK2ZAA1NpydpvQoAAtamwNQaEgADU2_018.jpg',
          name: '3'
        },
        {
          imgUrl: 'https://desk-fd.zol-img.com.cn/t_s960x600c5/g5/M00/03/01/ChMkJlv88omIdK2ZAA1NpydpvQoAAtamwNQaEgADU2_018.jpg',
          name: '4'
        }
      ],
      expandedDom: false,
    }
  },
  mounted(){
    this.changSwipeBtnShow(this.swipeList.length)
  },
  methods:{
    showHideDom(){
      this.expandedDom = true;
    },
    // 控制tab 标签的显示与隐藏
    changSwipeBtnShow(number){
      for(var i=0; i< number; i++){
        this.showSwipeBtn.push(false)
      }
    },
    openApp(){
      this.$router.push({name:'DownLoad',params:{id:"ss"}})
    },
    onSwipeItemIndexChange (index) {
      console.log('demo item change', index)
      //   /mobile/activity/member/addStatus
    },
    selectSwipe(i) {
      // this.changSwipeBtnShow(this.swipeList.length);
      let showBtn = this.showSwipeBtn[i] == false ? 'true' : false;
      this.showSwipeBtn.splice(i,1,showBtn);
    },
    changeSwipeItemIndex(i){
      this.swipeItemIndex = i;
      this.tagListContent(i,'video_tab_p','video_tab_select')
    },
    //点击标签添加背景色
    tagListContent(index,targetName,addClassName){
      var addBackground = document.getElementsByClassName(targetName);
      var domLen = addBackground.length;
      for(let i = 0; i < domLen; i++){
        if(index == i){
          this.addClass(addBackground[i],addClassName)
        }else{
          this.removeClass(addBackground[i],addClassName)
        }
      }
    },
    //判断是否有某个class
    hasClass( elements,cName ){
      return !!elements.className.match( new RegExp( "(\\s|^)" + cName + "(\\s|$)") ); // ( \\s|^ ) 判断前面是否有空格 （\\s | $ ）判断后面是否有空格 两个感叹号为转换为布尔值 以方便做判断
    },
    //添加class名
    addClass( elements,cName ){
      if( !this.hasClass( elements,cName ) ){
        elements.className += " " + cName;
      }
    },
    //删除class
    removeClass( elements,cName ){
      if( this.hasClass( elements,cName ) ){
        elements.className = elements.className.replace( new RegExp( "(\\s|^)" + cName + "(\\s|$)" )," " ); // replace方法是替换
      };
    },
    // 添加className
    changAddClass(i){
      this.tagListContent(i,'video_tab_second','video_tab_select')
    }
  }
}
</script>

<style scoped>
  html,body{
    height: 100%;
    width: 100%;
    padding-top: 30px;
    box-sizing: border-box;
  }
  .video_box_content{
    width: 100%;
    height: 100%;
    background: #cccccc;
    display: flex;
    flex-direction: column;
  }
  .video_head_image{
    height: 2.5rem;
    width: 100%;
    background: #cccccc;
    overflow: hidden;
  }
  .video_all_hidden{
    width: 100%;
    flex: 1;
  }
  .video_tab{
    width: 100%;
  }
  .video_tab_btn{
    width: 100%;
    padding: 0.04rem 0.1rem 0.1rem 0rem;
    box-sizing: border-box;
    background: #ffffff;
    display: flex;
    flex-wrap: wrap;
  }
  .video_tab_p,.video_tab_second{
    font-size: 0.15rem;
    padding: 0.02rem 0.06rem;
    border-radius: 0.06rem;
    border: 1px solid #333333;
    margin: 0.06rem 0rem 0rem 0.07rem;
  }
  .video_tab_content{
    width: 100%;
    max-height: 1rem;
    overflow: hidden;
    background: #ffffff;
  }
  .video_swipe_content{
    width: 100%;
    background: #ffffff;
    padding: 0rem 0.06rem 0.15rem 0.06rem;
    box-sizing: border-box;
    font-size: 0.14rem;
    text-wrap: normal;
    position: relative;
  }
  .video_tab_select{
    background: #FF6B00;
    color: #ffffff;
  }
  .video_swipe_show{
    height: 0.25rem;
    box-sizing: border-box;
    position: absolute;
    right: 0.15rem;
    bottom: 0.12rem;
    font-size: 0.14rem;
    color: #FF6B00;
  }
  .video_baseInformation{
    width: 100%;
    margin-top: 0.1rem;
    background: #ffffff;
  }
  .video_baseInformation_title{
    width: 100%;
    height: 0.3rem;
    font-size: 0.15rem;
    display: flex;
    align-items: center;
    padding: 0px 0.08rem;
    box-sizing: border-box;
    font-weight: bold;
  }
  .video_baseInformation_tab{
    width: 100%;
    display: flex;
    flex-wrap: wrap;
    padding: 0.04rem 0rem 0.1rem 0rem;
    box-sizing: border-box;
  }
  .concat_dom{
    width: 100%;
    height: 0.4rem;
    background: #ffffff;
    font-size: 0.15rem;
    display: flex;
    align-items: center;
    justify-content: center;
    cursor: pointer;
  }
  .concat_icon{
    height: 0.12rem;
    width: 0.12rem;
    border-left: 1px solid #666666;
    border-top: 1px solid #666666;
    transform: rotate(225deg);
    margin-top: -0.08rem;
    margin-right: 0.1rem;
  }
  .detail_splendid_content{
    width: 100%;
    background: rgba(255,255,255,1);
  }
  .detail_body_information_title{
    height: 0.33rem;
    width: 100%;
    display: flex;
    align-items: center;
    justify-content: flex-start;
    background:rgba(255,255,255,1);
    padding: 0.1rem 0rem 0rem 0rem;
    box-sizing: border-box;
  }
  .remove_padding{
    padding-top: 0px;
  }
  .detail_border_left{
    width: 0.04rem;
    height: 0.15rem;
    background:rgba(229,117,36,1);
    border-radius: 0.13rem;
    margin-right: 15px;
  }
  .detail_down_btn_box{
    height: 0.5rem;
    width: 100%;
    display: flex;
    align-items: center;
    justify-content: center;
  }
  .detail_down_btn{
    height: 0.4rem;
    flex: 1;
    margin: 0rem 0.15rem 0rem 0.15rem;
    box-sizing: border-box;
    background: #FF6B00;
    border-radius: 0.18rem;
    display: flex;
    align-items: center;
    justify-content: center;
    color: #FFFFFF;
    font-size: 0.16rem;
  }
  .detail_border_content{
    font-size: 0.14rem;
    font-weight: bold;
  }
  .video_magical_box{
    width: 100%;
    background:linear-gradient(180deg,rgba(38,38,38,0.53) 0%,rgba(53,53,53,1) 100%);
    display: flex;
    flex-direction: column;
  }
  .video_magical_list{
    height: 0.9rem;
    flex: 1;
    margin: 0.1rem 0.15rem 0rem 0.15rem;
    background: #FFFFFF;
    display: flex;
    align-items: center;
  }
  .video_magical_list_end{
    margin-bottom: 0.1rem;
  }
  .video_magical_content{
    height: 0.8rem;
    width: 100%;
    overflow: hidden;
    display: flex;
  }
  .video_magical_content_left{
    height: 0.8rem;
    flex: 1;
  }
  .magical_word{
    height: 0.6rem;
    width: 100%;
    display: flex;
    align-items: center;
    overflow: hidden;
    font-weight: bold;
    font-size: 0.15rem;
    padding: 0rem 0.01rem 0rem 0.04rem;
    box-sizing: border-box;
  }
  .magical_open_app{
    width: 0.8rem;
    height: 0.2rem;
    color: red;
    padding-left: 0.04rem;
    box-sizing: border-box;
  }
  .video_magical_content_right{
    height: 0.8rem;
    width: 1rem;
    background: red;
    display: flex;
    align-items: center;
    justify-content: center;
    overflow: hidden;
  }
  .video_magical_content_right img{
    height: 100%;
    width: auto;
  }
  .detail_body_lineBar{
    width: 100%;
    padding: 0rem 0.1rem 0.1rem 0.1rem;
    box-sizing: border-box;
    background:rgba(255,255,255,1);
    display: flex;
    flex-direction: column;
  }
  .video_lineBar_content{
    height: 0.2rem;
    width: 100%;
    display: flex;
    font-size: 0.15rem;
    align-items: center;
    margin-top: 0.1rem;
  }
  .video_lineBar_name{
    width: 0.47rem;
    height: 0.2rem;
  }
  .video_lineBar_number{
    width: 0.4rem;
    height: 100%;
    background:rgba(255,107,0,1);
    border-radius: 0.13rem;
    color:rgba(255,255,255,1);
    display: flex;
    align-items: center;
    justify-content: center;
  }
  .video_lineBar_barShow{
    width: 1.12rem;
    height: 0.05rem;
    display: flex;
    align-items: center;
    margin-left: 0.1rem;
    background:rgba(216,216,216,1);
    border-radius:3px;
    opacity:0.5305;
  }
  .video_lineBar_barShow_cover{
    height: 0.05rem;
    width: 0.6rem;
    background: #FF6B00;
    border-radius: 0.03rem;
  }
  .video_lineBar_info{
    flex: 1;
    height: 100%;
    margin-left: 0.05rem;
    overflow: hidden;
  }
  .video_select_list{
    width: 100%;
    margin-top: 0.1rem;
    background: white;
    font-size: 0.16rem;
    font-weight: bold;
    padding: 0.06rem 0rem 0.06rem 0rem;
    box-sizing: border-box;
  }
  .select_video_list{
    width: 100%;
    padding: 0rem 0.1rem 0rem 0.1rem;
    box-sizing: border-box;
    display: flex;
    flex-wrap: wrap;
    align-items: center;
    justify-content: space-between;
  }
  .select_list_first{
    width: 48%;
    height: 1.5rem;
  }
 .select_list_first_add{
   margin-top: 0.15rem;
 }
  .select_img_box{
    height: 1.3rem;
    width: 100%;
    display: flex;
    align-items: center;
    justify-content: center;
    overflow: hidden;
  }
  .select_img_box img{
    height: 100%;
    width: auto;
  }
  .select_img_name{
    height: 0.2rem;
    width: 100%;
    display: flex;
    align-items: center;
    justify-content: center;
  }
</style>
