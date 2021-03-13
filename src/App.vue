// TEMPLATES -------------------------------------------
<template lang="pug">
	#app
		Intro(
			@start-cv="opacityTotal = 1"
			v-if="opacityTotal === 0"
		)
		Waves
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
			opacityTotal: 0,
			x: 0,
			y: {0: 0, 1: 2, 2: 0, 3: 0, 4: 0, 5: 0, 6: 0, 7: 0,},
			opened: false,
			controlPermission: true,
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
						{name: 'Dmitry Pavlov',			desc: 'Frontend Vue, 24y.o.',				icon: '',		type: 'modal',},
						{name: 'About this Site',		desc: 'Stack and #src',					icon: '',		type: 'modal',},
					],
					[
						{name: 'MyGitHub',				desc: '',								icon: '',		type: 'modal',		link:'https://github.com/dmrompav',},
						{name: 'MyCodePen',				desc: '',								icon: '',		type: 'modal',		link:'https://codepen.io/trending',},
						{name: 'VueCRM',				desc: 'in process',						icon: '',		type: 'modal',},
						{name: 'JS site-constructor',	desc: 'in process',						icon: '',		type: 'modal',},
					],
					[
						{name: 'English',				desc: 'Intermediate',					icon: '',		type: 'modal',},
						{name: 'HTML',					desc: 'Pug + Semantic',					icon: '',		type: 'modal',},
						{name: 'CSS',					desc: 'SASS/Stylus',					icon: '',		type: 'modal',},
						{name: 'Tailwind',				desc: 'learning...',					icon: '',		type: 'no',},
						{name: 'JS (ES6+)',				desc: '',								icon: '',		type: 'modal',},
						{name: 'TypeScript',			desc: 'learning...',					icon: '',		type: 'no',},
						{name: 'Vue',					desc: 'Vue-cli, VueX',					icon: '',		type: 'modal',},
						{name: 'DX',					desc: 'git, bundlers, npm, IDE...',		icon: '',		type: 'modal',},
						{name: 'Soft skills',			desc: '',								icon: '',		type: 'modal'},
					],
					[
						{name: 'Eloquent javascript',	desc: 'Marijin Haverbeke',				icon: '',		type: 'no'},
						{name: 'Grokking algorithms',	desc: 'Aditia Bhargava',				icon: '',		type: 'no'},
					],
					[
						{name: 'Simple',				desc: '',								icon: '',		type: 'link',		link:'https://samara.hh.ru/resume/c6fd48e2ff08b5ed960039ed1f7a3251785048',},
						{name: 'Creative',				desc: 'in process',						icon: '',		type: 'no',},
					],
					[
						{name: 'Mum',					desc: 'My son is a good boy...',		icon: '',		type: 'modal',},
					],
					[
						{name: 'Phone',					desc: '+7(996) 107-88-23',				icon: '',		type: 'link',		link:'tel:+79961078823',},
						{name: 'Telegram',				desc: 'The most convinient',			icon: '',		type: 'link',		link:'',},
						{name: 'WhatsApp',				desc: '',								icon: '',		type: 'link',		link:'',},
						{name: 'Gmail',					desc: 'dm.rom.pav@gmail.com',			icon: '',		type: 'link',		link:'mailto:dm.rom.pav@gmail.com',},
					],
					[
						{name: 'Language',				desc: 'Eng => Rus in process',						icon: '',		type: 'no'},
						// {name: 'DarkBlue',				desc: 'Color theme',					icon: '',		type: 'script',		other: 'DarkRed',},
						{name: 'High Prefomace',		desc: 'click to enter this',			icon: '',		type: 'script',		liothernk: 'High Quality',},
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
							'',
							'',
							'',
							'',
							'',
							'',
							'',
							'',
						],
						1: [
							'', 
							'', 
							'', 
							'', 
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
							'', 
							'', 
							'', 
							'', 
							'', 
							'', 
							'', 
							'',
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
		horButClick(key) {this.x = key},
		verButClick(key, k) {
			this.y[key] = k
			this.openPopup()
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
					e.preventDefault();
					this.opened ? this.closePopup() : this.openPopup()
					break
			}
		},
		onWheel(e) {
			let delta = e.deltaY || e.detail || e.wheelDelta
			if(delta < 0 && this.y[this.x] > 0) {this.y[this.x]--}
			else if(delta > 0 && this.y[this.x] < this.admin.ver[this.x].length - 1) {this.y[this.x]++}
		},
	},
	mounted: function() {
		// keyup listener
		document.addEventListener('keydown', this.keyClick, false)
		// mousewheel listener
		if (window.addEventListener) {
			if ('this.onWheel' in document) {window.addEventListener("wheel", this.onWheel)}					// IE9+, FF17+, Ch31+
			else if ('onmousewheel' in document) {window.addEventListener("mousewheel", this.onWheel)}			// устаревший вариант события
			else {window.addEventListener("MozMousePixelScroll", this.onWheel)}									// Firefox < 17
		} else {window.attachEvent("onmousewheel", this.onWheel)}												// IE8-
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
	height 100vh
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
</style>
