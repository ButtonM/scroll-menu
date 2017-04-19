<template>
  <div class="hello">
    <div class="sortMenu clearfix" :scroll="scroll">
    	<div class="container" @mouseleave="scroll.isScroll = false">
    		<ul class="sortMenu-ul" :style="{ marginLeft: scroll.sortMenuUlLeft + 'px' }" @mouseenter="scroll.isScroll=true">
          <li class="cell" v-for="item in sortMenu">
            <a href="">{{item.sortname}}</a>
          </li>
        </ul>
        <transition name="fade">
          <div class="scroll-table"  v-show="scroll.isScroll" @mouseenter="scrollMousedown(0,240,0.38)" :style="{ left: scroll.scrollLeft + 'px' }"></div>
        </transition>
    	</div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'hello',
   data () {
    return {
      sortMenu: [
        { sortname: '全部' },
        { sortname: '家用电器家用电器' },
        { sortname: '家用电器家用电器' },
        { sortname: '生活用品' },
        { sortname: '食品' },
        { sortname: '美妆' },
        { sortname: '书籍' },
        { sortname: '洗护用品' },
        { sortname: '母婴用品' },
        { sortname: '家居' }
      ],
      sortName: [
        { sortname: '家用电器' },
        { sortname: '母婴' },
        { sortname: '百货' },
        { sortname: '珠宝配饰' },
        { sortname: '运动户外' },
        { sortname: '食品' },
        { sortname: '美妆' },
        { sortname: '家装' },
        { sortname: '家居家纺' },
        { sortname: '鲜花宠物' },
        { sortname: '图书乐器' },
        { sortname: '生活服务' },
        { sortname: '游戏动漫' }
      ],
      //滚动条参数
      scroll:{
      	//是否显示滚动条
      	isScroll:false,
      	//滚动条left
	      scrollLeft:0,
	      //导航left
	      sortMenuUlLeft:0,
      }
      
    }
  },
  created: function(){
  	
  },
  methods:{
    //判断鼠标位置 min 是最小的left max是最大的left menuleft是导航移动相当于滚动条的倍数
	    	scrollMousedown(MIN,MAX,MENULEFT){
  	      let vm = this;
  	      vm.scroll.isScroll = true;
  	      document.onmousedown = function(e){
		    		e = e? e:window.event;
		    		let oldScreenX = e.screenX - vm.scroll.scrollLeft;
		    		document.onmousemove = function(e){
		          e = e? e:window.event;
		          vm.scroll.scrollLeft = e.screenX-oldScreenX;
		          vm.scroll.sortMenuUlLeft = - MENULEFT*( e.screenX-oldScreenX);
		          if(vm.scroll.scrollLeft < MIN){
		          	vm.scroll.scrollLeft = MIN;
		          	vm.scroll.sortMenuUlLeft = MIN;
		          }else if(vm.scroll.scrollLeft  > MAX){
		          	vm.scroll.scrollLeft = MAX;
		          	vm.scroll.sortMenuUlLeft = - MENULEFT*MAX;
		          }
		    		}
			    	document.onmouseup = function(e){
			    		 this.onmousemove = null;
			    	}
	    	  }
  	    },
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
/* 分类菜单*/
*{
	margin:0;
	padding: 0;
}
#app{
	margin-top: 0;
}
body {
    -moz-user-select: none; /*火狐*/
    -webkit-user-select: none; /*webkit浏览器*/
    -ms-user-select: none; /*IE10*/
    -khtml-user-select: none; /*早期浏览器*/
    user-select: none;
}
.container{
	margin: 0 auto;
	width: 1200px;
	height: 65px;
	overflow: hidden;
}
ul{
	top: 0;
	left: 100px;
	list-style: none;
}
.sortMenu-ul{
	width:1500px;
	height: 50px;
}
.cell{
	float: left;
	width: 120px;
	height: 46px;
	line-height: 46px;
	padding: 2px 5px;
	background-color: rgba(44,62,80,0.6);
	border-bottom: 1px solid #2C3E50;
}
.cell:hover{
	background-color: rgba(44,62,80,0.8);
}
.cell a{
	display: block;
	color: #fff;
}
.scroll-table{
	position: relative;
	margin-top: -5px;
	width: 960px;
	height: 15px;
	border-radius:6px;
	background-color: rgba(44,62,80,0.7);
}
/*滚动条出现时的css*/
.fade-enter-active, .fade-leave-active {
  transition: opacity .5s
}
.fade-enter, .fade-leave-active {
  opacity: 0
}
</style>
