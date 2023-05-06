<template>
  <main class="form-signin w-25 m-auto mt-5">
    <form>
      <img
        :src="logo"
        alt="logo"
        style="width: 100px; cursor: pointer"
        @click="toHomeHandler"
      />
      <h1 class="h3 mb-3 fw-normal mt-3">Login</h1>
      <p
        v-if="email && password && passemail "
        class="list-group-item list-group list-group-item-danger mt-2"
      >
        Invalid email or password. Try again.
      </p>
      <Input :label="'Email address'" :type="'email'" v-model="email" />
      <ValidationError
        v-if="emails"
        :typeing="'Email'"
        :validationErrors="emails"
      />

      <Input :label="'Password'" :type="'password'" v-model="password" />
      <ValidationError
        v-if="passwords"
        :typeing="'Password'"
        :validationErrors="passwords"
      />
      <Button type="submit" :disabled="isLoading" @click="submitHandler"
        >Login</Button
      >
    </form>
  </main>
</template>

<script>
import { mapState } from "vuex";
import { logo } from "../contstants";
import ValidationError from "@/components/ValidationError.vue";
export default {
  data() {
    return {
      logo,
      email: "",
      password: "",
      emails: "",
      passwords: "",
      emorpass: "",
      passemail: false,
    };
  },
  components: {
    ValidationError,
  },
  computed: {
    ...mapState({
      isLoading: (state) => state.auth.isLoading,
      validationErrors: (state) => state.auth.errors,
    }),
  },
  methods: {
    submitHandler(e) {
      e.preventDefault();
      const data = {
        username: this.username,
        email: this.email,
        password: this.password,
      };
      this.$store
        .dispatch("login", data)
        .then((user) => {
          console.log("USER", user);
          this.$router.push({ name: "home" });
        })
        .catch(
          (err) => (
            (this.emails = err.errors.email),
            (this.passwords = err.errors.password),
            (this.emorpass = err.errors)
          )
        );
    },
  },
	updated(){
		console.log(this.passemail);
	}
};
</script>

<style></style>
