<template>
	<h1>PartyBox</h1>
	
	<HomePage :style="{ display: homeVisible }"
		@named="onTitleChange" />
	<FormPage :style="{ display: formVisible }"
		:party="party"
		:contacts="contacts"
		:drinks="drinks"
		:foods="foods"
		:other="other"
		@filled="onFormFilled" />
	<PartyDetails :style="{ display: detailsVisible }"
		:contacts="contacts"
		:details="party" />
	
</template>

<script>
import HomePage from './pages/Home.vue';
import FormPage from './pages/Form.vue';
import PartyDetails from './pages/PartyDetails.vue';

export default {
  name: 'App',
	components: {
		HomePage,
		FormPage,
		PartyDetails
	},
	data(){
		return {
			party: {
				title: "",
				local: "",
				datetime: {
					type: Date,
					default: new Date()
				},
				guestList: [],
				hostList: [],
				consumables: [[], [], []],
				theme: "",
				additionalNotes: ""
			},
			contacts: ['Fulano', 'Sicrano', 'Beltrano'],
			drinks: ['Whisky', 'Vodka', 'Aguardente', 'Cachaça'],
			foods: ['Brownie', 'Pizza Grande', 'Cento de Salgado'],
			other: ['Maconha 5g', 'Cigarro Dunhill', 'Narguile'],
			homeVisible: 'block',
			formVisible: 'none',
			detailsVisible: 'none'
		}
	},
	methods: {
		onTitleChange(newTitle){
			this.party.title = newTitle;
			this.toFormPage();
		},
		onFormFilled(filledForm){
			this.party = filledForm;
			this.toDetailsPage();
		},
		toFormPage(){
			this.homeVisible = "none";
			this.formVisible = "block";
			this.detailsVisible = "none";
		},
		toDetailsPage(){
			this.homeVisible = "none";
			this.formVisible = "none";
			this.detailsVisible = "block";
		}
	}
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Open+Sans&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Montserrat&display=swap');

h1, h2, button {
	font-family: "Montserrat", sans-serif;
}

h2 { text-align: center; }

label, li, ::placeholder {
	font-family: "Open Sans", sans-serif;
}

#app {
  color: #2c3e50;
}
</style>
