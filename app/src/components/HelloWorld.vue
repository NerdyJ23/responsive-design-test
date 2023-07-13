<template>
	<v-card color="#F0F9FF" elevation="0" style="height: 100vh">
		<v-card-text class="custom-font">
			<v-row class="mx-2">
				<v-col cols="12">
					<h1 class="py-10 custom-font custom-header custom-color" style="font-size:4em">Surf the Ocean</h1>
				</v-col>
			</v-row>
			<v-row class="mx-2">
				<v-col cols="12" md="4" class="d-flex flex-column">
					<random-image ref="imageRef"/>
					<v-btn class="ml-auto px-8 py-2 custom-color" @click="loadImage">New Image</v-btn>
					<span class="ml-auto subtitle">...provided by Pexels</span>
				</v-col>
				<v-col cols="12" md="4" class="d-flex flex-column">
					<h3 class="mt-auto">Send me to a friend!</h3>
					<div>
						<v-text-field outlined single-line placeholder="user@place.com" v-model="email" type="email"></v-text-field>
					</div>
					<v-btn class="ml-auto px-8 py-2 custom-font custom-color" @click="sendEmail">send</v-btn>
				</v-col>
			</v-row>
		</v-card-text>
	</v-card>
</template>
<script>
import RandomImage from './RandomImage.vue';
export default {
	name: "test",
	components: {
		RandomImage
	},
	data() {
		return {
			email: ""
		}
	},
	methods: {
		loadImage() {
			this.$refs.imageRef.loadImage();
		},
		getImageUrl() {
			return this.$refs.imageRef.getImage();
		},
		sendEmail() {
			const string = `mailto:${this.email}?subject=cool image&body=Look at this cool image i found! ${this.getImageUrl()}`;
			window.open(string);
		}
	}
}
</script>
<style>
@import url('https://fonts.googleapis.com/css2?family=DM+Sans&display=swap'); /* Google Fonts DM Sans */
.custom-color {
	color: #0369A1 !important;
}
.custom-header {
	font-size: 54px !important;
}
.custom-font {
	font-family: 'DM Sans' !important;
}
h3 {
	color: #0369A1 !important;
	font-size: 24px;
}
.subtitle {
	font-size: 14px;
}
</style>