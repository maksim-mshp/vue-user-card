<template>
	<div id="app">
		<UserCard
			v-if="show"
			:address="address"
			:email="email"
			:image="image"
			:name="name"
			:phone="phone"
			:username="username"
		></UserCard>
	</div>
</template>

<script>
import UserCard from "./components/UserCard.vue";

export default {
	name: "App",
	components: {
		UserCard,
	},
	data() {
		return {
			show: false,
			image: "/70.jpg",
			username: "romashka",
			name: "Иванов Иван Иванович",
			address: "Москва, Юбилейная 50",
			email: "coldrabbit48@example.com",
			phone: "+7-495-266-57-34",

			user: {},
		};
	},
	methods: {
		getUser() {
			this.axios.get("https://api.randomuser.me/").then((response) => {
				this.user = response.data.results[0];

				this.image = this.user.picture.large;
				this.username = this.user.login.username;
				this.name = this.user.name.first + ' ' + this.user.name.last;
				this.address = this.user.location.city + ', ' + this.user.location.street.name + ', ' + this.user.location.street.number;
				this.email = this.user.email;
				this.phone = this.user.phone;

				this.show = true;
			});
		},
	},
	created() {
		this.getUser();
	},
};
</script>

<style></style>
