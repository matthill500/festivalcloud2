<template>
<div>
    <div id="noCognitoMessage" class="configMessage" style="display: none;">
            <div class="backdrop"></div>
            <div class="panel panel-default">
                <div class="panel-heading">
                    <h3 class="panel-title">No Cognito User Pool Configured</h3>
                </div>
                <div class="panel-body">
                    <p>There is no user pool configured in <a href="/js/config.js">/js/config.js</a>. You'll configure this in Module 2 of the workshop.</p>
                </div>
            </div>
        </div>

        <header>
         
        </header>

        <section class="form-wrap">
            <h1>Register</h1>
            <form id="registrationForm">
              <input type="email" id="email" placeholder="Email" pattern=".*" style="margin: 10px;" required><br>
              <input type="password" id="password1" placeholder="Password" style="margin: 10px;" pattern=".*" required><br>
              <input type="password" id="password2" placeholder="Confirm Password" style="margin: 10px;"  pattern=".*" required><br>


              <input type="submit" value="Register" v-on:click="handleRegister()" style="margin: 10px;">
            </form>
        </section>
    </div>
</template>

<script>
// import HelloWorld from "@/components/HelloWorld.vue";
export default {
  name: "Register",
  components: {
    // HelloWorl
  },
  data(){
      return{
          form:{
              email: "",
              password1: "",
              password2: ""
          }
      }
  },
  methods:{
       handleRegister(event) {
        var email = this.form.email;
        var password = this.form.password1;
        var password2 = this.form.password2;

        var onSuccess = function registerSuccess(result) {
            var cognitoUser = result.user;
            console.log('user name is ' + cognitoUser.getUsername());
            var confirmation = ('Registration successful. Please check your email inbox or spam folder for your verification code.');
            if (confirmation) {
                window.location.href = 'verify.html';
            }
        };
        var onFailure = function registerFailure(err) {
            alert(err);
        };
        event.preventDefault();

        if (password === password2) {
            register(email, password, onSuccess, onFailure);
        } else {
            alert('Passwords do not match');
        }
    }
  }
};
</script>