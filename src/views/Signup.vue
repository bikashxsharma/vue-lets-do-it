<template>
	<div class="signup">
		<h2>Signup</h2>
		<input
			type="text"
			placeholder="Email"
			v-model="email"
			required
		/>
		<br />
		<input
			type="text"
			placeholder="Full Name"
			v-model="fullName"
			required
		/>
		<br />
		<input
			type="password"
			placeholder="Password"
			v-model="password"
			required
		/>
		<br />
		<p v-if="error">{{ error }}</p>
		<button v-on:click="signUp">
			Signup
		</button>
		<p>
			If you already have an account
			<router-link to="/login"
				>Login</router-link
			>
		</p>
	</div>
</template>
<script>
import firebase from 'firebase'
export default {
	name: 'Signup',
	data: function() {
		return {
			email: '',
			fullName: '',
			password: '',
			error: '',
		}
	},
	methods: {
		signUp() {
			if (
				this.email !== '' &&
				this.fullName !== '' &&
				this.password !== ''
			) {
				firebase
					.auth()
					.createUserWithEmailAndPassword(
						this.email,
						this.password,
					)
					.then((data) =>
					firebase.database()
						console.log(
							'Data',
							data.user,
							data.user.uid,
						),
					)
					.catch(
						(err) =>
							(this.error =
								err.message),
					)
			} else {
				alert(
					'Enter both email and pass',
				)
			}
		},
	},
}
</script>
<style scoped>
.signup {
	margin: auto;
	margin-top: 60px;
	text-align: center;
}
.signup input {
	margin: 10px;
	padding: 10px;
}
.signup button {
	margin: 10px;
	padding: 10px;
}
.signup .signup__illustration {
	margin-bottom: 20px;
}
</style>
