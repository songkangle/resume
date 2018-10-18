<template>
	<div id="app">
		<div id="content">
			<StyleEditor ref="styleEditor" :code="currentStyle"></StyleEditor>
		</div>
		<ResumeEditor ref="resumeEditor" :markdown="currentMarkdown" :enableHtml="enableHtml"></ResumeEditor>
		<!-- <div id="foot">
      <ThankEditor ref="thankEditor" :markdown="currentThankMarkdown" :enableHtml="enableHtml"></ThankEditor>
    </div> -->
	</div>
</template>

<script>
	import StyleEditor from './components/StyleEditor'
	import ResumeEditor from './components/ResumeEditor'
	import './assets/reset.css'

	export default {
		name: 'app',
		components: {
			StyleEditor,
			ResumeEditor
		},
		data() {
			return {
				interval: 5,
				currentStyle: '',
				enableHtml: false,
				fullStyle: [
`/*
* 大家好，我是宋康乐。
* 我来写一份简历！
*/

/* 给所有元素加上过渡效果 */
* {
  transition: all .1s;
}
/* 设置背景颜色 */
html {
  background: url("https://songkangle.github.io/weixin_node/timg.jpg") no-repeat center center;
  background-size: cover;
}
#content{
  height:70vh;
  margin:0;
}
#foot{
  height:29vh;
  margin:0;
}

/* 设置边框 */
.styleEditor {
  padding: .5em;
  border: 1px solid;
  margin: .5em;
  overflow: auto;
  width: 50vw; height: 70vh;
  background: rgb(20,20,20);
}
/* 代码高亮 */
.token.selector{ color: rgb(130,150,0); }
.token.property{ color: rgb(190,140,0); }
.token.punctuation{ color: yellow; }
.token.function{ color: rgb(40,160,150); }

/* 加3D效果 */
html{
  perspective: 1000px;
}
.styleEditor {
  position: fixed; left: 0; top: 0;
  -webkit-transition: none;
  transition: none;
  -webkit-transform: rotateY(10deg) translateZ(-100px) ;
          transform: rotateY(10deg) translateZ(-100px) ;
}

/* 准备一个编辑器 */
.resumeEditor{
  position: fixed; right: 0; top: 0;
  padding: .5em;  margin: .5em;
  width: 50vw; height: 70vh;
  border: 1px solid;
  background: rgb(200,200,200); color: #222;
  overflow: auto;
  -webkit-transition: none;
  transition: none;
  -webkit-transform: rotateY(-10deg) translateZ(-100px) ;
          transform: rotateY(-10deg) translateZ(-100px) ;
}
/* 开始写简历 */
`,
					`
/*将Markdown格式翻译成HTML
 *再对HTML加点样式
*/
.resumeEditor{
  padding: 2em;
}
.resumeEditor h2{
  display: inline-block;
  border-bottom: 1px solid;
  margin: 1em 0 .5em;
}
.resumeEditor ul,.resumeEditor ol{
  list-style: none;
}
.resumeEditor ul> li::before{
  content: '•';
  margin-right: .5em;
}
.resumeEditor ol {
  counter-reset: section;
}
.resumeEditor ol li::before {
  counter-increment: section;
  content: counters(section, ".") " ";
  margin-right: .5em;
}
.resumeEditor blockquote {
  margin: 1em;
  padding: .5em;
  background: #ddd;
}
`,
`/* 写封感谢信。
 * 感谢大家对我的关注。
 */
.styleEditor{
    width:50vw;height:70vh;
}

.resumeEditor{
   width:50vw;height:70vh;
}

.thankEditor{
  position: relative; left: 0; top: 0;
  background: #E9D9BB;
  color: #001C42;
  overflow: auto;
}

.thankEditor {
  width: 99vw; height: 45vh;
  border: 1px solid #ccc;
  font-size: .9em;
}
`,
					`
.thankEditor{
  padding: .5em;  margin: .5em; margin-top:1em;
}

.thankEditor ul,.thankEditor ol{
  list-style: none;
}
.thankEditor ul> li::before{
  content: '☞'; color: red;
  margin-right: .5em;
}
.thankEditor ol {
  counter-reset: section;
}
.thankEditor ol li::before {
  counter-increment: section;
  content: counters(section, "☞") " ";
  margin-right: .5em;
}

.thankEditor{
  width: 99vw; height: 45vh;
  -webkit-transition: none;
  transition: none;
  -webkit-transform: rotateX(-10deg) translateZ(-200px);
          transform: rotateX(-10deg) translateZ(-200px);
}
`
				],
				currentMarkdown: '',
				fullMarkdown: `宋康乐
====
求职：
前端工程师。

技能
====
 	★★★★★★★★ 
    ★★★★★★
★技术及语言★
    ★★★★
	★★★
	★★
	★
----
  - H5，Css3,Jquery，
  - Vue，React，Angular(玩过基于Angular语法的ionic)，
  - gulp，webpack，git，
  - Less，Sass，
  - node，python（会一点爬虫），了解一点php，
  - MySQL，mongodb
  - React native(学习中...)
  - 公众号开发
  - 小程序开发
----

Project introduction
----
    - 2016-06~2017-09
    - 公众号：宁波云游国际
	- 技术：html，css，Js，Jq
	- 功能：提供旅游服务的产品
	- 项目链接地址：微信公众号(宁波云游国际旅行社)，包括pc端 http://yunyou.unohacha.com/
⚡⚡⚡⚡⚡⚡
    - 2017-04~2017-05
    - pc端：矩恩生物
    - 技术：html，css，js，JQ，
    - 功能：一个医疗的官网
    - 项目链接地址：http://www.gujinyiguan.com/
⚡⚡⚡⚡⚡⚡
	- 2017-06~2017-09
    - pc：夸克优富
	- 技术：html,css,js,JQ
	- 功能：一款金融的官网
	- 项目链接地址：http://www.quarkwealth.com/
⚡⚡⚡⚡⚡⚡
	- 2017-9~2017-10
    - pc：巨涛生物科技
	- 技术：html,css,js,JQ
	- 功能：一款粮食的官网
    - 项目链接地址：http://www.hzpaana.com.cn/
⚡⚡⚡⚡⚡⚡
	- 2017-11~2017-12
	- pc：趣理财后台管理系统（不断更新迭代）
	- 技术: vue,element,axios,echarts,es6,less,webpack
	- 功能：一款供内部使用的后台管理系统，包括用户管理，授信管理，提现管理，贷后管理，运营管理，财务管理，系统管理
	- 项目链接地址：内部系统不便提供，详情面试细谈。 
⚡⚡⚡⚡⚡⚡
	- 2018-01~2018-02
	- 小程序：记账
	- 技术：小程序原生框架，
	- 功能：一款给老板使用的记账小程序
	- 项目链接地址：
⚡⚡⚡⚡⚡⚡
	 - 2018-03~2018-04
	 - 移动wap：初租商户端
	 - 技术：vue,mint,axios,echarts,es6,less,webpack
	 - 功能：就是给线下用的回收手机的应用。
	 - 项目链接地址：下架了
⚡⚡⚡⚡⚡⚡
	 - 2018-06~2018-07(更新维护)
	 - PC：收啊后台管理系统
	 - 技术：vue,element,axios,echarts,es6,less,webpack
	 - 功能：一款供内部使用的后台管理系统，包括用户管理，贷后管理，运营管理，财务管理，系统管理
	 - 项目链接地址：内部系统。。。。。。
⚡⚡⚡⚡⚡⚡
	 - 2018-07~2018-08
	 - 小程序：学习react
	 - 技术：react
	 - 项目链接地址：自己写这玩，源码可见https://www.cnblogs.com/sklhtml/
⚡⚡⚡⚡⚡⚡
	 - 2018-09~2018-10
	 - 小程序：梦想清单
	 - 技术：小程序,node，express，mysql，
	 - 功能：一个地方的三级分销购物平台
	 - 项目链接地址：自己写这玩，源码可见https://www.cnblogs.com/sklhtml/
⚡⚡⚡⚡⚡⚡
	 - 2017-10~至今
	 - 负责公司内部所有的H5，包括app内部的h5页面，运营的推广页面等等。
				

Work Experience
====

1. 吾诺瀚卓
2. 杭州万家乐科技


Educational Experience
====

1. 西安外事学院

Blog
====

* [GitHub](https://github.com/songkangle)
* [个人博客](https://www.cnblogs.com/sklhtml/)


Contact Me
====
* 电话：13018915505
* 微信：13186188929
* QQ：912643012

----

* 我还年轻，我渴望上路，带着最初的激情，追寻着最初的梦想，感受着最初的梦想
* on the road。 
`
			}
		},
		created() {
			this.makeResume()
		},

		methods: {
			makeResume: async function() {
				await this.progressivelyShowStyle(0);
				await this.progressivelyShowResume();
				await this.progressivelyShowStyle(1);
				await this.showHtml();
				await this.progressivelyShowStyle(2);
				await this.progressivelyShowThanks();
				await this.progressivelyShowStyle(3)
			},
			showHtml() {
				return new Promise((resolve, reject) => {
					this.enableHtml = true
					resolve()
				})
			},
			progressivelyShowStyle(n) {
				return new Promise((resolve, reject) => {


					// 异步处理
    				// 成功调用resolve 往下传递参数 且只接受一个参数
    				// 失败调用reject  往下传递参数 且只接受一个参数


					let interval = this.interval
					let showStyle = (async function() {
						let style = this.fullStyle[n]
						if(!style) {
							return
						}
						// 计算前 n 个 style 的字符总数
						console.log()

						// filter也是一个常用的操作，它用于把Array的某些元素过滤掉，然后返回剩下的元素。
						// reduce计算数组元素相加后的总和：




						let length = this.fullStyle.filter((_, index) => index <= n).map((item) => item.length)
						.reduce((p, c) => p + c, 0)


						let prefixLength = length - style.length
						if(this.currentStyle.length < length) {
							let l = this.currentStyle.length - prefixLength
							let char = style.substring(l, l + 1) || ' '
							this.currentStyle += char
							if(style.substring(l - 1, l) === '\n' && this.$refs.styleEditor) {
								this.$nextTick(() => {
									this.$refs.styleEditor.goBottom()
								})
							}
							setTimeout(showStyle, interval)
						} else {
							resolve()
						}
					}).bind(this)
					showStyle()
				})
			},
			progressivelyShowResume() {
				return new Promise((resolve, reject) => {
					let length = this.fullMarkdown.length
					let interval = this.interval
					let showResume = () => {
						if(this.currentMarkdown.length < length) {
							this.currentMarkdown = this.fullMarkdown.substring(0, this.currentMarkdown.length + 1)
							let lastChar = this.currentMarkdown[this.currentMarkdown.length - 1]
							let prevChar = this.currentMarkdown[this.currentMarkdown.length - 2]
							if(prevChar === '\n' && this.$refs.resumeEditor) {
								this.$nextTick(() => this.$refs.resumeEditor.goBottom())
							}
							setTimeout(showResume, interval)
						} else {
							resolve()
						}
					}
					showResume()
				})
			},
			progressivelyShowThanks() {
				return new Promise((resolve, reject) => {
					let length = this.thanksMarkdown.length
					let interval = this.interval
					let showThanks = () => {
						if(this.currentThankMarkdown.length < length) {
							this.currentThankMarkdown = this.thanksMarkdown.substring(0, this.currentThankMarkdown.length + 1)
							let lastChar = this.currentThankMarkdown[this.currentThankMarkdown.length - 1]
							let prevChar = this.currentThankMarkdown[this.currentThankMarkdown.length - 2]
							if(prevChar === '\n' && this.$refs.thankEditor) {
								this.$nextTick(() => this.$refs.thankEditor.goBottom())
							}
							setTimeout(showThanks, interval)
						} else {
							resolve()
						}
					}
					showThanks()
				})
			}
		}
	}
</script>

<style scoped>
	#app {
		font-family: 'Avenir', Helvetica, Arial, sans-serif;
		-webkit-font-smoothing: antialiased;
		-moz-osx-font-smoothing: grayscale;
	}
	
	html {
		min-height: 100vh;
	}
	
	* {
		box-sizing: border-box;
	}
</style>