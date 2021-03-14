// TEMPLATES -------------------------------------------
<template lang="pug">
	.ver-sliders(
		:class="`ver-sliders--${x}`"
	)
		transition-group(name="ver-slider__appear" tag="div")
			nav.ver-slider(
				v-for="(item, key) in ver"
				:key="key"
				v-show="key === x"
				:class="`ver-slider--${key} ver-slider-position--${y[key]}`"
			)
				li.ver-slider__li(
					v-for="(i, k) in ver[key]"
					:key="k"
				)
					button.ver-btn.clicknull(
						v-if="ver[key][k].type !== 'link'"
						:class="(k === y[key])? 'ver-btn--selected' : 'ver-btn--selectable'"
						:style="ver[key][k].type === 'no' ? 'cursor: not-allowed !important' : ''"
						@click="$emit('select', key, k, $event)"
					)
						.ver-btn__icon(
							:style="`background-position: -${ver[key][k].icon[0] * 60}px -${ver[key][k].icon[1]  * 60}px;`"
						)
						.ver-btn__txt
							h3.ver-btn__name {{ ver[key][k].name }}
							p.ver-btn__desc {{ ver[key][k].desc }}
					a.ver-btn.clicknull(
						v-if="ver[key][k].type === 'link'"
						target="_blank"
						:href="ver[key][k].link"
						:class="(k === y[key])? 'ver-btn--selected' : 'ver-btn--selectable'"
						:style="ver[key][k].type === 'no' ? 'cursor: not-allowed !important' : ''"
						@click="$emit('select', key, k, $event)"
					)
						.ver-btn__icon(
							:style="`background-position: -${ver[key][k].icon[0] * 60}px -${ver[key][k].icon[1]  * 60}px;`"
						)
						.ver-btn__txt
							h3.ver-btn__name {{ ver[key][k].name }}
							p.ver-btn__desc {{ ver[key][k].desc }}
					hr.ver-slider__hr(v-if="key === 1 && k === 1")
</template>



// SCRIPTS -------------------------------------------
<script>
export default {
	name: 'VerSliders',
	props: {
		x: 		Number, 
		y:		Object,
		ver:	Array,
	},
}
</script>



// STYLES -------------------------------------------
<style scoped lang="stylus">
$size = 60px
$ml = 60px
$quantity = 0..7					//how much sliders
$quantityY = 0..10					//how much buttons

$translateX(n)						// !mixin - translate ver-sliderS
	val = (- n * 180)px
	.ver-sliders--{n}
		transform translate(val)
$sliderPos(n)						// !mixin - position forEach ver-slider_
	val = (n * 180)px
	.ver-slider--{n}
		transform translate(val)
$translateY(n)						// !mixin - translate ver-slider_ up-down
	val = (- n * 100)px
	.ver-slider-position--{n}
		top val

// Styles =======
.ver-sliders
	z-index: 30
	position absolute
	transition transform 0.2s
	@media (min-width: 601px) and (min-height: 601px)
		top 30vh
		left 30vw
	@media (max-width: 600px),(max-height: 600px)
		top 70px
		left 10vw

for one in $quantity
	$translateX(one)
	
.ver-slider
	position absolute
	@media (min-width: 601px) and (min-height: 601px)
		margin-left $ml
	display flex
	flex-direction column
	justify-content flex-start
	align-items flex-start
	opacity 1
	transition top 0.2s

	&__hr
		width 60px
		height 3px
		background-color #fff
		margin -7px 0 10px 0

for one in $quantity
	$sliderPos(one)
for one in $quantityY
	$translateY(one)
	// &__li

.ver-btn
	display flex
	flex-direction row
	justify-content flex-start
	align-items center
	transition margin-top 0.1s

	&__icon
		position relative
		width $size
		height $size
		background-color #35495e
		border-radius 30%
		margin 10px 20px 30px 0px
		@media (min-width: 601px) and (min-height: 601px)
			filter grayscale(90%)
		transition transform 0.15s
		background-image url('./../assets/ps/ver_min.jpg')

		&:after
			content ''
			position absolute
			top 0
			left 0
			width $size 
			height $size
			border 2px solid #fff
			border-radius 30%

	&__txt
		width 400px
		max-width 65vw

	&__name
		text-align left
		font-size 22px
		transition font-size 0.15s

	&__desc
		width 100%
		text-align left
		font-size 18px
		word-wrap wrap
		transition font-size 0.15s

	&--selectable
		&:hover>.ver-btn__icon
			@media (min-width: 601px) and (min-height: 601px)
				transform scale(1.2)
				filter grayscale(60%)
		&:hover>.ver-btn__txt>.ver-btn__name
			@media (min-width: 601px) and (min-height: 601px)
				font-size 24px
		&:hover>.ver-btn__txt>.ver-btn__desc
			@media (min-width: 601px) and (min-height: 601px)
				font-size 20px

	&--selected
		@media (min-width: 601px) and (min-height: 601px)
			margin-top 160px
		&>.ver-btn__icon
			@media (min-width: 601px) and (min-height: 601px)
				transform scale(1.2)
				filter grayscale(0%)
		&>.ver-btn__txt>.ver-btn__name
			@media (min-width: 601px) and (min-height: 601px)
				font-size 24px
		&>.ver-btn__txt>.ver-btn__desc
			@media (min-width: 601px) and (min-height: 601px)
				font-size 20px

// Animation -----
.ver-slider__appear
	&-enter,
	&-leave-to
		opacity 0
	&-enter-active, 
	&-leave-active
		transition opacity 0.2s
	&-enter-to,
	&-leave
		opacity 1
</style>
