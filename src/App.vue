// TEMPLATES -------------------------------------------
<template lang="pug">
	#app(
		:style="`height: ${H}px;`"
	)
		Intro(
			@start-cv="opacityTotal = 1"
			v-if="opacityTotal === 0"
		)
		Waves(
			v-if="canvas.exist"
		)
		transition(name="container-appear")
			.opacity-container(
				v-show="opacityTotal"
			)
				HorSlider(
					:x="x"
					:hor="admin.hor"
					@select="horButClick"
				) 
				VerSliders(
					:x="x"
					:y="y"
					:ver="admin.ver"
					@select="verButClick"
				) 
				Modal(
					:x="x"
					:y="y"
					:ver="admin.ver"
					:modal="admin.modal"
					:opened="opened"
					@closePopup="closePopup"
				)
				SlideCount(
					:x="x"
					:quantity="horLength"
				)
		address.info FrontendCV LastUpdate: March 11, 2021
</template>



// SCRIPTS -------------------------------------------
<script> 
import Intro		from './components/Intro.vue'
import Waves		from './components/Waves.vue'
import HorSlider	from './components/HorSlider.vue'
import VerSliders	from './components/VerSliders.vue'
import Modal		from './components/Modal.vue'
import SlideCount	from './components/SlideCount.vue'


export default {
	name: 'App',
	components: {
		Intro, Waves, HorSlider, VerSliders, Modal, SlideCount
	},
	data() {
		return {
			canvas: {
				exist: true,
			},
			H: Number,
			opacityTotal: 0,
			x: 0,
			y: {0: 0, 1: 2, 2: 0, 3: 0, 4: 0, 5: 0, 6: 0, 7: 0,},
			opened: false,
			control: {
				pos: {
					x0: Number,
					y0: Number,
					x: Number,
					y: Number,
				},
				clickPermission: true,
				swipePermission: true,
				swipeRoute: 'none',
				isItSwipeNow: false,
				alredyHorSwiped: false,
				whatY: Number,
				howMuchToSwi: 20,
				howMuchToVerSwi: 40
			},
			admin: {
				intro: {
					h1: 'Frontend CV',
					caption: 'Made with',
				},
				hor: [
					{name: 'Info', 			icon: '0'},
					{name: 'Projects', 		icon: '1'},
					{name: 'Skills', 		icon: '2'},
					{name: 'Read books', 	icon: '3'},
					{name: 'Download CV', 	icon: '4'},
					{name: 'Rating', 		icon: '5'},
					{name: 'Contact me', 	icon: '6'},
					{name: 'Settings', 		icon: '7'},
				],
				ver: [
					[
						{name: 'Dmitry Pavlov',			desc: 'Frontend Vue, 24y.o.',			icon: [0,1],		type: 'modal',},
						{name: 'About this Site',		desc: 'Stack and #src',					icon: [0,2],		type: 'modal',},
					],
					[
						{name: 'MyGitHub',				desc: '',								icon: [1,0],		type: 'link',		link:'https://github.com/dmrompav',},
						{name: 'MyCodePen',				desc: '',								icon: [1,1],		type: 'link',		link:'https://codepen.io/dmrompav',},
						{name: 'VueCRM',				desc: 'in process...',					icon: [1,2],		type: 'modal',},
						{name: 'JS site-constructor',	desc: 'in process...',					icon: [1,3],		type: 'modal',},
					],
					[
						{name: 'English',				desc: 'Intermediate',					icon: [2,0],		type: 'modal',},
						{name: 'HTML',					desc: 'Pug + Semantic',					icon: [2,1],		type: 'modal',},
						{name: 'CSS',					desc: 'SASS/Stylus',					icon: [2,2],		type: 'modal',},
						{name: 'Tailwind',				desc: 'learning...',					icon: [2,3],		type: 'no',},
						{name: 'JS (ES6+)',				desc: '',								icon: [3,0],		type: 'modal',},
						{name: 'TypeScript',			desc: 'learning...',					icon: [3,1],		type: 'no',},
						{name: 'Vue',					desc: 'Vue-cli, VueX',					icon: [3,2],		type: 'modal',},
						{name: 'Canvas',				desc: 'Animations',						icon: [0,0],		type: 'modal',},
						{name: 'DX',					desc: 'git, bundlers, npm, IDE...',		icon: [3,3],		type: 'modal',},
						{name: 'Soft skills',			desc: '',								icon: [4,2],		type: 'modal'},
					],
					[
						{name: 'Eloquent javascript',	desc: 'Marijin Haverbeke',				icon: [0,3],		type: 'no'},
						{name: 'Grokking algorithms',	desc: 'Aditia Bhargava',				icon: [0,4],		type: 'no'},
					],
					[
						{name: 'Simple',				desc: '',								icon: [4,0],		type: 'link',		link:'https://samara.hh.ru/resume/c6fd48e2ff08b5ed960039ed1f7a3251785048',},
						{name: 'Creative',				desc: 'in process...',					icon: [4,1],		type: 'no',},
					],
					[
						{name: 'Mum',					desc: 'My son is a good boy...',		icon: [1,4],		type: 'modal',},
					],
					[
						{name: 'Phone',					desc: '+7(996) 107-88-23',				icon: [4,3],		type: 'link',		link:'tel:+79961078823',},
						{name: 'Telegram',				desc: 'The most convinient',			icon: [2,4],		type: 'link',		link:'',},
						{name: 'WhatsApp',				desc: '',								icon: [3,4],		type: 'link',		link:'',},
						{name: 'Gmail',					desc: 'dm.rom.pav@gmail.com',			icon: [4,4],		type: 'link',		link:'mailto:dm.rom.pav@gmail.com',},
					],
					[
						{name: 'Language',				desc: 'in process...',					icon: [2,0],		type: 'no'},
						// {name: 'DarkBlue',				desc: 'Color theme',					icon: '',			type: 'script',		other: 'DarkRed',},
						{name: 'High Perfomace',		desc: 'click to enter this',			icon: [0,0],		type: 'script',		script: this.SCRIPT1,		other: 'High Quality',},
					],
				],
				modal: {
					icons: {
						1: [[1,1], [1,2], [1,3], [1,4], [1,5], [1,6], [1,7], [1,8],],
						2: [[2,1], [2,2], [2,3], [2,4], [2,5], [2,6], [2,7], [2,8],],
						3: [[3,1], [3,2], [3,3], [3,4], [3,5], [3,6], [3,7], [3,8],],
						4: [[4,1], [4,2], [4,3], [4,4], [4,5], [4,6], [4,7], [4,8],],
						5: [[5,1], [5,2], [5,3], [5,4], [5,5], [5,6], [5,7], [5,8],],
						6: [[6,1], [6,2], [6,3], [6,4], [6,5], [6,6], [6,7], [6,8],],
						7: [[7,1], [7,2], [7,3], [7,4], [7,5], [7,6], [7,7], [7,8],],
						8: [[8,1], [8,2], [8,3], [8,4], [8,5], [8,6], [8,7], [8,8],],
					},
					text: {
						0: [
							'<p></p>',
							'<p></p>',
						],
						1: [
							'', 
							'', 
							'',
							'', 
						],
						2: [
							'', 
							'', 
							'', 
							'', 
							'', 
							'', 
							'', 
							'',
						],
						3: [
							'', 
							'', 
							'', 
							'', 
							'', 
							'', 
							'', 
							'',
						],
						4: [
							'', 
							'', 
							'', 
							'', 
							'', 
							'', 
							'', 
							'',
						],
						5: [
							'<p>My son is good boy and succesful programmer. He can install windows and fix the printer.</p>', 
						],
						6: [
							'', 
							'', 
							'', 
							'', 
							'', 
							'', 
							'', 
							'',
						],
						7: [
							'', 
							'', 
							'', 
							'', 
							'', 
							'', 
							'', 
							'',
						],
					},
				}
			}
		}
	},
	computed: {
		horLength() {return this.admin.hor.length},
	},
	methods: {
		resize() {this.H = window.innerHeight},
		horButClick(key) {this.x = key},
		verButClick(key, k) {
			this.y[key] = k
			this.enterThisBtn()
		},
		closePopup() {this.opened = false},
		openPopup() {
			if(this.admin.ver[this.x][this.y[this.x]].type === 'modal') {
				this.opened = true
			}
		},
		keyClick(e) {
			switch(e.key) {
				case 'ArrowLeft':
					if(!this.opened && this.x > 0) this.x--
					break
				case 'ArrowRight':
					if(!this.opened && this.x < this.admin.hor.length - 1) this.x++
					break
				case 'ArrowUp':
					if(!this.opened && this.y[this.x] > 0) this.y[this.x]--
					break
				case 'ArrowDown':
					if(!this.opened && this.y[this.x] < this.admin.ver[this.x].length - 1) this.y[this.x]++
					break
				case 'Enter':
					e.preventDefault()
					if(this.admin.ver[this.x][this.y[this.x]].type === "link") {
						window.open(this.admin.ver[this.x][this.y[this.x]].link, "_blank")
					} else {
						this.enterThisBtn()
					}
					break
			}
		},
		enterThisBtn() {
			if(this.admin.ver[this.x][this.y[this.x]].type === "modal") {
				this.opened ? this.closePopup() : this.openPopup()
			} else if(this.admin.ver[this.x][this.y[this.x]].type === "script") {
				this.admin.ver[this.x][this.y[this.x]].script()
			}
		},
		onWheel(e) {
			if(!this.opened) {
				e.preventDefault()
				let delta = e.deltaY || e.detail || e.wheelDelta
				if(delta < 0 && this.y[this.x] > 0) {this.y[this.x]--}
				else if(delta > 0 && this.y[this.x] < this.admin.ver[this.x].length - 1) {this.y[this.x]++}
			}
		},
		touchStart(e) {
			this.clickPermission = true
			this.control.pos.x0 = e.touches[0].pageX
			this.control.pos.y0 = e.touches[0].pageY
			this.whatY = this.y[this.x]
		},
		touchMove(e) {
			e.preventDefault()
			if(!this.opened) {
				let x = e.changedTouches[0].pageX,
					y = e.changedTouches[0].pageY,
					deltaX = x - this.control.pos.x0,
					deltaY = y - this.control.pos.y0

				if(!this.control.isItSwipeNow) {
					if((Math.abs(deltaX) > this.control.howMuchToSwi || Math.abs(deltaY) > this.control.howMuchToSwi)) {
						this.control.isItSwipeNow = true
					}
				}

				if(this.control.swipeRoute === 'none') {
					if(this.control.isItSwipeNow) {
						this.control.swipeRoute = (Math.abs(deltaX) < Math.abs(deltaY))? 'ver': 'hor'
					}
				} else {
					if(this.control.swipeRoute === 'hor') {
						if(!this.control.alredyHorSwiped) {
							if(deltaX > 0 && this.x > 0) {
								this.x--
								this.control.alredyHorSwiped = true
							} else if(deltaX < 0 && this.x < this.admin.hor.length - 1) {
								this.x++
								this.control.alredyHorSwiped = true
							}
						}
						
					} else if(this.control.swipeRoute === 'ver'){
						let newVerPos = this.whatY - ((deltaY - deltaY % this.control.howMuchToVerSwi)/this.control.howMuchToVerSwi)
						if(newVerPos < 0) {
							newVerPos = 0
						} else if(newVerPos > this.admin.ver[this.x].length - 1) {
							newVerPos = this.admin.ver[this.x].length - 1
						}
						this.y[this.x] = newVerPos
					}
				}
			}
		},
		touchEnd() {
			this.control.swipeRoute = 'none'
			this.control.alredyHorSwiped = false
		},
		SCRIPT1() {
			this.canvas.exist = !this.canvas.exist
			let a = this.admin.ver[this.x][this.y[this.x]].name
			this.admin.ver[this.x][this.y[this.x]].name = this.admin.ver[this.x][this.y[this.x]].other
			this.admin.ver[this.x][this.y[this.x]].other = a
			console.log(this.admin.ver[this.x][this.y[this.x]].name)
			console.log(this.admin.ver[this.x][this.y[this.x]].other)
		}
	},
	mounted: function() {
		// resize listener to set 100vh (mobile)
		window.addEventListener('resize', this.resize)
		this.resize()
		// keyup listener
		document.addEventListener('keyup', this.keyClick, {passive: false})
		// mousewheel listener
		if ('this.onWheel' in document) {window.addEventListener("wheel", this.onWheel, {passive: false})}						// IE9+, FF17+, Ch31+
		else if ('onmousewheel' in document) {window.addEventListener("mousewheel", this.onWheel, {passive: false})}			// устаревший вариант события
		else {window.addEventListener("MozMousePixelScroll", this.onWheel, {passive: false})}									// Firefox < 17
		// touch listeners
		document.addEventListener("touchstart", this.touchStart)
		document.addEventListener("touchmove", this.touchMove, {passive: false})
		document.addEventListener("touchend", this.touchEnd)
	},
}
</script>



// STYLES -------------------------------------------
<style lang="stylus">
@import './assets/_reset.styl'
@font-face
	font-family PO
	src url('./assets/fonts/PoiretOne-Regular.woff2') format('woff'), url('./assets/fonts/PoiretOne-Regular.woff') format('woff')

//Styles ========
#app 
	display block
	position fixed
	width 100vw
	// height 100vh
	background-color #000
	color #fff
	font-family PO
	user-select none

.info 
	position absolute
	z-index 100
	bottom 0
	left 0
	width 100vw
	height 18px
	line-height 18px
	background rgba(0, 0, 0, 0.6)
	text-align center
	font-style normal

.container-appear
	&-enter,
	&-leave-to
		opacity 0
	&-enter-active,
	&-leave-active
		transition opacity 0.5s
	&-enter-to,
	&-leave
		opacity 1


// other =====
.pop-up__context>p 
	font-size 20px
	margin-top 15px
	animation lazy 0.2s linear
	@keyframe lazy
		0% 
			opacity 0
			transform translate(-300px)
		100% 
			opacity 1
			transform translate(0px)
</style>
