<template lang="html">
	<div class="player">
		<div class="name">
			<p v-bind:class='{isDead: player.dead}'> Name:</p>
			<input type="text" v-model='player.name'>
			<p v-bind:class='{isDead: player.dead}' v-show='player.dead'>DEAD</p>
		</div>
		<div class="life">
			<p>Life: </p>
			<input type="number" v-model.number='player.life'>
		</div>
		<div class="poison">
			<p>Poison: </p>
			<input type="number" min='0' v-model.number='player.poison'>
		</div>
		<div class="comDeaths">
			<p>Commander has died: </p>
			<input type="number" min='0' v-model.number='player.comDeaths'><pre> times</pre>
			<p>adding {{player.comDeaths * 2}} mana</p>
		</div>
		<h5>Commander Damage</h5>
		<div class="commanderDmg" v-for='(name, index) in playerArray'>
			<div class="comDmg" v-if='name.id != player.id' >
				<p>{{name.name}}</p>
				<input type="number" min='0' v-model='player.comDmg[index]'>
			</div>
		</div>
	</div>
</template>

<script>
export default {
	name: 'Player',
	props: {
		player:{
			type: Object,
			required: true
		},
		playerArray: {
			type: Array,
			required: true
		}
	},
	watch: {
		'player.life': function(){this.player.dead = this.iThinkWereJustDeadHere()},
		'player.poison': function(){this.player.dead = this.iThinkWereJustDeadHere()},
		'player.comDmg': function(){this.player.dead = this.iThinkWereJustDeadHere()}

	},
	data () {
		return {

		}
	},
	methods: {
		iThinkWereJustDeadHere: function(){
			for(var i = 0; i < this.player.comDmg.length; i++) {
				if(this.player.comDmg[i] >= 21){
					return true;
				}
			}
			if(this.player.life <= 0 || this.player.poison >= 10){
				return true;
			} else {
				return false;

			}

		}
	}
}
</script>

<style scoped lang="sass">
	.player
		border-bottom: 1px solid rgba(white, 0.85)
		margin: 16px 8px
		padding: 8px
	p, pre
		color: rgba(white,0.85)
		display: inline-block
		margin-bottom: 0
		&.isDead
			color: rgba(#7c0000, 0.85)
	div>input
		width: 60px
	.name>input
		width: 120px
	.comDeaths>p:last-child
		display: block
		margin-bottom: 16px
		margin-top: 0

	.comDeaths>input
		margin: 0
	h5
		color: rgba(#fff,0.85)
		font-weight: 400
		margin: 0
</style>
