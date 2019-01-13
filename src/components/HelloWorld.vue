<template>
  <div class="hello container is-desktop">
    <div v-if="errors">
      <ul v-for="error in errors" :key="error.id">
        <li>
          <p>{{error}}</p>
        </li>
      </ul>
    </div>
    <form @submit="checkForm" action="#" method="post">
      <div class="field">
        <label class="label">E-Mail</label>
        <div class="control">
          <input class="input" type="email" placeholder="Your E-Mail" name="email">
        </div>
      </div>
      <div class="field">
        <label class="label">Password</label>
        <div class="control">
          <input class="input" type="text" placeholder="Password">
        </div>
      </div>
      <div class="field">
        <button class="button" type="submit" @click="register">Register</button>
      </div>
    </form>
  </div>
</template>

<script>
import { AmplifyEventBus } from "aws-amplify-vue";
export default {
  name: "HelloWorld",
  data() {
    return {
      email: "",
      password: "",
      errors: []
    };
  },
  created() {
    AmplifyEventBus.$on("authState", info => {
      console.log("Emitted event", info);
    });
  },
  methods: {
    checkForm() {
      let rexPw = new RegExp("^(?=.*[a-z])(?=.*[A-Z])(?=.*d)[a-zA-Zd]{8,}$");
      if (this.email && this.password) {
        if (rexPw.test(this.password)) {
          return true;
        } else {
          this.errors = [];
          this.errors.push(
            "Enter a password that contains at least: \n - one uppercase letter \n - one lowercase letter \n - one number"
          );
        }
      }
      if (!this.email) {
        this.errors.push("E-Mail is required.");
      }
      if (!this.password) {
        this.errors.push(
          "Enter a password that contains at least: \n - one uppercase letter \n - one lowercase letter \n - one number"
        );
      }
      e.preventDefault();
    },
    register() {}
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
