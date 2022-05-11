<template>
<div>
	<h2>Formulário</h2>
	<form @submit.prevent=sendDetails(childParty)>	
		<label for="local">Local</label>
		<input id="local" 
			v-model="childParty.local" 
			placeholder="Espaço Miriam" 
			required/>

		<label for="datetime">Dia e hora</label>
		<input id="datetime" 
			type="datetime-local" 
			v-model="childParty.datetime"
			required/>

		<label for="hosts">Anfitrião(ões)</label>
		<select id="hosts" 
			name="hosts" 
			v-model="childParty.hostList" 
			multiple>
			<option v-for="host in contacts" :key="host">
				{{ host }}
			</option>
		</select>

		<label for="guests">Convidados</label>
		<select id="guests" 
			name="guests" 
			v-model="childParty.guestList" 
			multiple>
			<option v-for="guest in contacts" :key="guest">
				{{ guest }}
			</option>
		</select>


		<label for="drinks">Bebidas</label>
		<select id="drinks"
			name="consumDrinks"
			v-model="childParty.consumables[0]" 
			multiple>
			<option v-for="drink in drinks" :key="drink">
				{{ drink }}
			</option>
		</select>

		<label for="foods">Comidas</label>
		<select id="foods"
			name="consumFoods"
			v-model="childParty.consumables[1]" 
			multiple>
			<option v-for="food in foods" :key="food">
				{{ food }}
			</option>
		</select>

		<label for="other">Outros</label>
		<select id="other"
			name="consums"
			v-model="childParty.consumables[2]" 
			multiple>
			<option v-for="drug in other" :key="drug">
				{{ drug }}
			</option>
		</select>

		<label for="theme">Tema do evento</label>
		<input id="theme" 
			v-model="childParty.theme" 
			placeholder="Festa Junina"/>
		
		<label for="notes">Notas Adicionais</label>
		<textarea id="notes" 
			v-model="childParty.additionalNotes" 
			rows="5"
			cols="10"
			placeholder="..."/>

		<button type="submit">Enviar</button>
	</form>
</div>
</template>

<script>
export default {
	name: 'FormPage',
	emits: ['filled'],
	props: {
		party: Object,
		contacts: Array,
		drinks: Array,
		foods: Array,
		other: Array
	},
	data(){
		return {
			childParty: this.party,
			today: new Date()
		};
	},
	methods: {
		sendDetails(){
			const localFieldEmpty = (this.childParty.local === '');
			const datetimeFieldEmpty = (this.childParty.datetime === '');

			this.childParty.datetime = new Date(this.childParty.datetime);

			if(localFieldEmpty || datetimeFieldEmpty){
				window.location.reload();
			}else{
				this.$emit('filled', this.childParty);
			}
		}
	}
}
</script>

<style scoped>
form {
	display: flex;
	flex-direction: column;
	align-items: stretch;
	padding: 10vw;
}

label { align-self: flex-start; }

input, textarea, select {
	margin-bottom: 5vh;
	width: 100%;
}

button {
	width: 40vw;
	height: 3.5vh;
	
}
</style>
