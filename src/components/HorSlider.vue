// TEMPLATES -------------------------------------------
<template lang="pug">
	.hor-slider
		button.arrow.arrow_left.clicknull(
			v-if="x !== 0"
			@click="$emit('select', x - 1)"
		) <
		button.arrow.arrow_right.clicknull(
			v-if="x !== hor.length - 1"
			@click="$emit('select', x + 1)"
		) >
		nav.hor-slider__nav(
			:class="`hor-slider--${x}`"
		)
			ul.hor-slider__ul
				li.hor-slider__li(
					v-for="(item, key) in hor"
					:key="key"
				)
					button.hor-btn.clicknull(
						@click="$emit('select', key)"
						:class="(key === x)? 'hor-btn--selected' : 'hor-btn--selectable'"
					)
						.hor-btn__icon(
							:style="`background-position: -${hor[key].icon * 84}px;`"
						)
						h2.hor-btn__txt {{ item.name }}
</template>



// SCRIPTS -------------------------------------------
<script>
export default {
	name: 'HorSlider',
	props: {
		x: Number,
		hor: Array,
	},
}
</script>



// STYLES -------------------------------------------
<style scoped lang="stylus">
$size = 90px 					//button size
$between = 0px 45px 8px 45px	//space between buttons
$quantity = 0..7				//how much buttons
$translate(n)					// !mixin - translate hor-slider
	val = (- n * 180)px
	valForMobile = (- n * 100)vw
	.hor-slider--{n}
		@media(min-width: 601px)
			transform translate(val)
		@media(max-width: 600px)
			left valForMobile !important

//Styles ========
.arrow
	@media(min-width: 601px)
		display none
	@media(max-width: 600px)
		position absolute
		z-index 50
		top 0px
		display block
		color #fff
		font-size 40px
		line-height 60px
		padding 0 10px

	&_left
		left 0
		
	&_right
		right 0

.hor-slider
	position absolute
	width 100vw
	height 100vh

	&__nav
		z-index 40
		position absolute
		left 30vw
		@media(min-width: 601px)
			top 30vh
		@media(max-width: 600px)
			top 0
			background rgba(0, 0, 0, 0.6)
		transition transform 0.2s

	&__ul
		display flex
		flex-direction row
		justify-content flex-start
		align-items flex-start

	// &__li

// !mixin - translate hor-slider
for one in $quantity
	$translate(one)

.hor-btn
	display flex
	flex-direction column
	justify-content flex-start
	align-items center
	transition transform 0.15s
	@media(max-width: 600px)
		width 100vw
		height 60px
		justify-content center
		cursor: default

	&__icon
		@media(min-width: 601px)
			width $size
			height $size
			background-color #42b883
			border 3px solid #fff
			border-radius 30%
			margin $between
			filter grayscale(60%)
			background-image url('./../assets/ps/hor.jpg')
			background-size 800%
		@media(max-width: 600px)
			display none

	&__txt
		width $size
		@media(max-width: 600px)
			width auto
			line-height 60px
		font-size 22px
		text-shadow 0 0 2px #fff, 0 0 4px #fff, 0 0 8px #fff, 0 0 16px #fff
		transform scale(0)
		transition transform 0.15s

	&--selectable
		&:hover
			transform scale(1.2)
		&:hover>.hor-btn__icon
			transform scale(1)
			filter grayscale(0%)
		&:hover>.hor-btn__txt
			transform scale(1)
	&--selected
		transform scale(1.2)
		&>.hor-btn__txt
			transform scale(1)
		&>.hor-btn__icon
			filter grayscale(0%)

</style>
