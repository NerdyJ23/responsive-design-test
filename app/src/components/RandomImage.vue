<template>
	<v-img contain v-if="image" :src="image" max-height="50vh" class="rounded-large" content-class="roundedImage" name="image"/>
	<div v-else style="height: 50vh">
		debug height words
	</div>
</template>
<script>
export default {
	name: "RandomImage",
	data() {
		return {
			image: null,
			api: "https://api.pexels.com/v1/",
			key: "3f1krjomBOrGCzqXRot4uZtjRtwCw49VbBqdiagcISd91VKh9NUmUZdu" //this will be disabled in 1 week for security as this is being published publicly
		}
	},
	mounted() {
		this.loadImage()
	},
	methods: {
		async loadImage() {

			//get curated list and count of how many photos exist, this does double our API requests however
			const response = await fetch(`${this.api}/search?query=ocean`, {
				headers: {
					"Authorization": this.key
				}
			});
			const data = await response.json();
			console.log(data);
			const randomNumber = Math.floor(Math.random() * data.total_results);
			console.log(randomNumber);

			const imageResponse = await fetch(`${this.api}/search?query=ocean&per_page=1&page=${randomNumber}`, {
				headers: {
					"Authorization": this.key
				}
			});
			const imageData = await imageResponse.json();

			const randomImage = imageData.photos[0];
			console.log(randomImage);

			//one last fetch, this time the image blob, non-api this time
			this.image = randomImage.src.medium;
		},
		getImage() {
			return this.image;
		}
	}
}
</script>
<style>
.roundedImage {
	border-radius: 24px;
}
</style>