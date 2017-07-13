<template lang="html">
	<div id="number">
		<p>Number of players: </p>
		<input type="number" min="0" v-model.number="numPlayers" >
		<div class="players">
			<player v-for="player in players" v-bind:player='player' v-bind:playerArray='players'></player>
		</div>
	</div>
</template>

<script>

function PlayerData(id) {
	this.id = id
	this.name = "";
	this.dead = false;
	this.life = 40;
	this.comDeaths = 0;
	this.comDmg = [];
	this.poison = 0;
}

import Player from './player.vue'


export default {
	name: 'Players',
	components: {
		'player': Player
	},
	data () {
		return {
			numPlayers: 0,
			players: [],
			counter: 0
		}
	},
	watch: {
		numPlayers: function(){this.getPlayers()}
	},
	methods: {
		getPlayers: function() {
			if(this.numPlayers > this.players.length) {
				for(var i = 0; i < this.numPlayers - this.players.length; i++) {
					this.players.push(new PlayerData(this.counter));
					this.counter++;
				}
			} else if (this.numPlayers < this.players.length) {
				for(var i = this.players.length; i > this.numPlayers; i--) {
					this.players.pop();
				}
			}
			for(var i = 0; i < this.players.length; i++){
				for(var j = 0; j < this.players.length; j++){
					if(this.players[i].comDmg.length < this.players.length) {
						this.players[i].comDmg.push(0);
					} else if(this.players[i].comDmg.length > this.players.length) {
						this.players[i].comDmg.pop();
					}
				}
			}
		}
	}
}
</script>

<style scoped lang="sass">
p
	color: rgba(white,0.85)
	display: inline-block
input
	width: 64px
.players
	display: flex
	justify-content: space-around
	flex-wrap: wrap
</style>
