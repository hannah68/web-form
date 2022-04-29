<template>
	<form @submit.prevent="handleSubmit">
		<label>Email:</label>
		<input type="email" v-model="email" />

		<label>Password:</label>
		<input type="password" v-model="password" />
		<div v-if="passwordError" class="error">{{ passwordError }}</div>

		<label>Role:</label>
		<select v-model="role">
			<option value="default">Select a Role</option>
			<option value="developer">Web Developer</option>
			<option value="designer">Web Designer</option>
		</select>

		<!-- keyborad event -->
		<label>Skills</label>
		<input type="text" v-model="tempSkill" @keyup="addSkill" />
		<div v-for="skill in skills" :key="skill" class="pill">
			<span @Click="deleteSkill(skill)">{{ skill }}</span>
		</div>

		<!-- one single checkbox (boolean)-->
		<div class="terms">
			<input type="checkbox" v-model="terms" />
			<label>Accept terms and conditions</label>
		</div>
		<!-- multiple input fields with checkbox (array)-->
		<!-- <div>
            <input type="checkbox" v-model="names" value="Hanna">
            <label>Hanna</label>
        </div>
        <div>
            <input type="checkbox" v-model="names" value="Reza">
            <label>Reza</label>
        </div>
        <div>
            <input type="checkbox" v-model="names" value="Ali">
            <label>Ali</label>
        </div> -->

		<div class="submit">
			<button>Create an account</button>
		</div>
	</form>

	<!-- <p>email: {{ email }}</p>
	<p>pass: {{ password }}</p>
    <p>role: {{ role }}</p>
    <p>terms: {{ terms }}</p>
    <p>names: {{ names }}</p>
    <p>tempSkill: {{ tempSkill }}</p>
    <p>skills: {{ skills }}</p> -->
</template>

<script>
	export default {
		data() {
			return {
				email: "",
				password: "",
				role: "default",
				terms: false,
				names: [],
				tempSkill: "",
				skills: [],
				passwordError: "",
			};
		},
		methods: {
			addSkill(e) {
				if (e.key === "," && this.tempSkill) {
					if (!this.skills.includes(this.tempSkill)) {
						this.skills.push(this.tempSkill);
					}
					this.tempSkill = "";
				}
			},
			deleteSkill(skill) {
				this.skills = this.skills.filter((el) => el !== skill);
			},
			handleSubmit() {
				// validate password
				this.passwordError =
					this.password.length > 5
						? ""
						: "Password must be atleast 6 chars long";
				if (!this.passwordError) {
					console.log("email", this.email);
					console.log("password", this.password);
					console.log("role", this.role);
					console.log("skills", this.skills);
					console.log("terms", this.terms);
				}
			},
		},
	};
</script>

// to keep track of input data(v-model). two way data binding: If the value
updates from input by the user, we bind that update to the component data, so
that the component data updates.

<style>
	form {
		max-width: 420px;
		margin: 30px auto;
		background: #fff;
		text-align: left;
		padding: 40px;
		border-radius: 10px;
	}
	label {
		color: #aaa;
		display: inline-block;
		margin: 25px 0 15px;
		font-size: 0.6rem;
		text-transform: uppercase;
		letter-spacing: 1px;
		font-weight: bold;
	}
	input,
	select {
		display: block;
		padding: 10px 6px;
		width: 100%;
		box-sizing: border-box;
		border: none;
		border-bottom: 1px solid #ddd;
		color: #555;
	}
	input[type="checkbox"] {
		display: inline-block;
		width: 16px;
		margin: 0 10px 0 0;
		position: relative;
		top: 2px;
	}
	.pill {
		display: inline-block;
		margin: 20px 10px 0 0;
		padding: 6px 12px;
		background: #eee;
		border-radius: 20px;
		font-size: 12px;
		font-weight: bold;
		color: #777;
		cursor: pointer;
	}
	button {
		background: #0b6dff;
		border: 0;
		padding: 10px 20px;
		margin-top: 20px;
		color: #fff;
		border-radius: 20px;
	}
	.submit {
		text-align: center;
	}
	.error {
		color: #ff0062;
		margin-top: 10px;
		font-size: 0.8rem;
		font-weight: bold;
	}
</style>
