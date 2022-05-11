<template>
<div>
	<h2>Olá, este é o PartyBox</h2>
	<form @submit.prevent=nameParty(title)>
		<label for="title">Qual nome você quer dar para o seu evento?</label>
		<input id="title" 
			v-model="title" 
			placeholder="Festa Junina"
			required/>
		<button type="submit">Nomear</button>
	</form>
</div>
</template>

<script>
export default {
	name: 'HomePage',
	emits: ['named'],
	data(){
		return{
			title: ""
		}
	},
	methods: {
		nameParty(){
			if(this.title === ''){
				window.location.reload();
			}else{
				this.$emit('named', this.title);
			}
		}
	},
}
</script>

<style scoped>
form {
	display: flex;
	flex-direction: column;
	align-items: center;
	padding: 10vw;
}

input {
	margin-bottom: 5vh;
	width: 100%;
}

button {
	width: 40vw;
	height: 3.5vh;
}
</style>
