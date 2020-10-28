<template>
	<div class="login">
		<h2>Login</h2>
		<input
			type="text"
			placeholder="Email"
			v-model="email"
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
		<button v-on:click="login">
			Login
		</button>
		<p>
			If you do not have an account,
			<router-link to="/signup"
				>create one.</router-link
			>
		</p>
	</div>
</template>
<script>
import firebase from 'firebase'
export default {
	name: 'Login',
	data: function() {
		return {
			email: '',
			password: '',
			error: '',
		}
	},
	methods: {
		login() {
			if (
				this.email !== '' &&
				this.password !== ''
			) {
				firebase
					.auth()
					.signInWithEmailAndPassword(
						this.email,
						this.password,
					)
					.then((data) =>
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
.login {
	margin: auto;
	margin-top: 60px;
	text-align: center;
}
.login input {
	margin: 10px;
	padding: 10px;
}
.login button {
	margin: 10px;
	padding: 10px;
}
.login .login__illustration {
	margin-bottom: 20px;
}
</style>
