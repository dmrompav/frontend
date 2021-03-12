// TEMPLATES -------------------------------------------
<template lang="pug">
	transition(name="modal__appear")
		.modal(v-if="opened")
			.tapfield.clicknull(
				@click.only="$emit('closePopup')"
			)
			.pop-up
				button.pop-up__exit.clicknull(
					@click="$emit('closePopup')"
				) back
				.pop-up__header 
					h3.pop-up__h3 {{ ver[x][y[x]].name }}
					.pop-up__icons
				.pop-up__context {{ modal.text[x][y[x]] }}
</template>



// SCRIPTS -------------------------------------------
<script>
export default {
	name: 'Modal',
	props: {
		x: Number,
		y: Object,
		ver: Array,
		modal: Object,
		opened: Boolean,
	},
}
</script>



// STYLES -------------------------------------------
<style scoped lang="stylus">
.modal 
	z-index 60
	position absolute
	width 100vw
	height 100vh
	opacity 1
	filter: blur(0px)
	backdrop-filter: blur(8px)

.tapfield
	position absolute
	width 100vw
	height 100vh
	background rgba(0, 0, 0, .3)
	cursor pointer

.pop-up
	position absolute
	width 800px
	max-width 95vw
	height auto 
	max-height 95vh
	padding 20px
	border 1px solid #ffffff
	border-radius 10px
	left 50vw
	top 50vh
	transform translate(-50%, -50%)
	overflow-x hidden
	overflow-y auto
	background-color rgba(53, 73, 94, 0.7)

	&__header
		max-width 70%

	&__exit
		position absolute
		top 20px
		right 20px
		font-size 26px
		font-weight 900
		width 65px
		height 28px
		border 1px solid #fff
		border-radius 20%

	&__h3
		font-size 26px
		font-weight 900

	// &__icons

	&__context
		position relative

// animation
.modal__appear
	&-enter
		opacity 0
		filter: blur(34px)
	&-enter-active
		transition opacity 0.2s, filter 0.6s ease-out 
	&-enter-to,
	&-leave
		opacity 1
		filter: blur(0px)
	&-leave-active
		transition opacity 0.6s, filter 0.2s 
	&-leave-to
		opacity 0
		filter: blur(34px)
		z-index 10

</style>
