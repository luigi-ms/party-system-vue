<template>
<div>
	<h2>Detalhes da Festa</h2>
	<ul>
		<li class="detail">
			<h3>Titulo:</h3>
			<span class="info" v-if="details.title !== ''">{{ details.title }}</span>
			<span class="info" v-else>Evento Sem Título</span>
		</li>

		<li class="detail">
			<h3>Local:</h3>
			<span class="info" v-if="details.local !== ''">{{ details.local }}</span>
			<span class="info" v-else>Evento Sem Local</span>
		</li>
		
		<li class="detail">
			<h3>Data e Hora:</h3>
			<span class="info" v-if="typeof details.datetime === 'object'">
				{{ details.datetime.toLocaleString() }}
			</span>
			<span class="info" v-else>Data e Hora Não Selecionadas</span>
		</li>
		
		<li class="detail">
			<h3>Convidados:</h3>
			<div class="info" v-if="details.guestList.length > 0">
				<ul>
					<li v-for="guest in details.guestList" :key="guest">
						{{ guest }}
					</li>
				</ul>
			</div>
			<div class="info" v-else>Evento Sem Convidados</div>
		</li>
		
		<li class="detail">
			<h3>Anfitrião(ões):</h3>
			<div class="info" v-if="details.hostList.length > 0">
				<ul>
					<li v-for="host in details.hostList" :key="host">
						{{ host }}
					</li>
				</ul>
			</div>
			<div class="info" v-else>Evento Sem Anfitrião (???)</div>
		</li>
		
		<li class="detail">
			<h3>Consumíveis:</h3>
			<div id="consums"
				class="info" 
				v-if="details.consumables.length > 0">
				<ul v-for="category in details.consumables" :key="category">
					<li v-for="consum in category" :key="consum">
						{{ consum }}
					</li>
				</ul>
			</div>
			<span class="info" v-else>Evento Sem Consumíveis</span>
		</li>
		
		<li class="detail">
			<h3>Tema:</h3>
			<span class="info" v-if="details.theme !== ''">{{ details.theme }}</span>
			<span class="info" v-else>Evento Sem Tema</span>
		</li>
		
		<li class="detail">
			<h3>Notas Adicionais:</h3>
			<span class="info" v-if="details.additionalNotes !== ''">{{ details.additionalNotes }}</span>
			<span class="info" v-else>Sem Notas</span>
		</li>
	</ul>
</div>
</template>

<script>
export default {
	name: 'PartyDetails',
	props: {
		details: Object
	}
}
</script>

<style scoped>
ul {
	list-style-type: none;
	padding: 8vw;
}

li {
	display: flex;
	justify-content: space-between;
	align-items: center;
}

.info {
	display: inherit;
	justify-content: flex-end;
	width: 50%;
}

#consums, #consums > ul {
	display: flex;
	flex-direction: column;
	align-items: flex-end;
}

h3 { 
	font-size: 1em;
	width: 50%;
}
</style>
