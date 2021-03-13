// TEMPLATES -------------------------------------------
<template lang="pug">
	.slide-count
		.point(
			v-for="i in quantity"
			:class="(i - 1 === x) ? 'point--selected' : ''"
		)
</template>



// SCRIPTS -------------------------------------------
<script>
export default {
	name: 'SlideCount',
	props: {
		quantity: Number,
		x: Number,
	}
}
</script>



// STYLES -------------------------------------------
<style scoped lang="stylus"> 
.slide-count
	position absolute
	left 0
	bottom 24px
	width 100vw
	height 15px
	display flex
	justify-content center
	align-items center
	
.point
	width 10px
	height 10px
	margin 0 2px
	background rgb(53, 73, 94)
	border 2px solid #fff
	border-radius 50%
	transition all 0.1s

	&--selected
		width 15px
		height 15px

</style>