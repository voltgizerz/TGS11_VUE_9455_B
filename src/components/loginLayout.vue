<template>
  <v-container>
    <v-card>
      <v-container grid-list-md mb-8 mt-5>
        <h1 class="text-md-center">Login Page - JWT</h1>
        <h5 class="text-md-center">(JSON WEB TOKEN)</h5>
        <v-layout row wrap style="margin:10px" justify="center">
          <v-row>
            <v-col cols="12">
              <v-text-field label="Email*" v-model="form.email" required></v-text-field>
            </v-col>
            <v-col cols="12">
              <v-text-field label="Password*" v-model="form.password" type="password" required></v-text-field>
            </v-col>
            <v-btn @click="login()" block color="green" height="40" width="10">LOGIN</v-btn>
          </v-row>
        </v-layout>
      </v-container>
    </v-card>
  </v-container>
</template>



<script>
export default {
  data() {
    return {
      form: {
        email: "",
        password: ""
      },
      user: new FormData()
    };
  },
  methods: {
    login() {
      var url = this.$apiUrl + "/Auth";

      this.user = new FormData();
      this.user.append("email", this.form.email);
      this.user.append("password", this.form.password);

      this.$http.post(url, this.user).then(response => {
        if (response.data.token) {
          alert("Success Login!");
          localStorage.setItem("token", response.data.token);
          this.$router.push({ name: "UserController" });
        } else {
          alert("Email or Password Invalid!");
        }
      });
    }
  }
};
</script>
