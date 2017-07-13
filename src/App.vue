<template lang="html">
	<div class="app-root">
		<h1>Commander Counter</h1>
		<players></players>
	</div>
</template>

<script>

import Players from './components/players.vue'

export default {
	name: 'app',
	components: {
		'players': Players
	},
	data () {
		return {

		}
	}
}
</script>

<style lang="sass">
	=transition($t)
		transition: all #{$t} cubic-bezier(.25,.8,.25,1)
	*
		border: none
		outline: none
		box-sizing: border-box
		font-family: 'Spectral', serif
	html, body
		background-color: #222

	input[type='text'], input[type='number']
		background-color: rgba(white, 0.85)
		padding: 2px 4px
		+transition(0.3s)
		&:hover, &:focus, &:active
			background-color: rgba(white, 0.95)
</style>

<style scoped lang="sass">
	h1
		font-size: 32px
		color: rgba(white, 0.85)
</style>
