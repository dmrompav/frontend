// TEMPLATES -------------------------------------------
<template lang="pug">
	.intro
		transition(name="curtain-appear")
			.curtain(
				v-if="introStarted"
			)
		transition(name="text-appear")
			.text(
					v-if="introStarted"
				)
				h1.h1 Frontend C
					|
					font.h1__font V
				p.h1__desc Dmitry Pavlov
</template>



// SCRIPTS -------------------------------------------
<script>
export default {
	name: 'Intro',
	data() {
		return {
			introStarted: false,
		}
	},
	mounted: function() {
		this.introStarted = true
		setTimeout(() => {
			this.introStarted = false
		}, 2500)
		setTimeout(() => {
			this.$emit('start-cv')
		}, 3000)
	}
}
</script>



// STYLES -------------------------------------------
<style scoped lang="stylus">
.intro 
	z-index 100
	position absolute
	width 100vw
	height 100vh

	display flex
	justify-content center
	align-items center

.curtain
	position absolute
	z-index 5
	width 100vw
	height 100vh
	background rgba(0, 0, 0, .5)
	backdrop-filter: blur(8px)

.text
	position absolute
	z-index 10

.h1
	font-size 45px
	@media (min-width 601px)
		font-size 80px
	font-weight 700
	&__font
		font-family sans-serif
		color rgb(66, 184, 131)
		&:before
			content 'v'
			color rgb(53, 73, 94)
			position absolute 
			z-index -1
			transform translate(12%, -17%)

// animation --------
.curtain-appear
	&-enter,
	&-leave-to
		opacity 0
	&-enter-active
		transition opacity 0.5s 0.5s
	&-enter-to,
	&-leave
		opacity 1
	&-leave-active
		transition opacity 0.5s

.text-appear
	&-enter
		transform scale(0.4)
		opacity 0
	&-enter-active
		transition transform 0.5s ease 0.5s, opacity 0.5s 0.6s
	&-enter-to,
	&-leave
		transform scale(1)
		opacity 1
	&-leave-active
		transition transform 0.5s, opacity 0.2s
	&-leave-to
		transform scale(0.4)
		opacity 0
</style>
