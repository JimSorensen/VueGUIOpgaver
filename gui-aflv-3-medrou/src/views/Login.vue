<template>
  <div>
        <div>
            <h1>This is an login page</h1>
            <input type="text" name="email" v-model="input.email" placeholder="email"/>
            <input type="password" name="password" v-model="input.password" placeholder="Kodeord"/>
            <button type="button" v-on:click="login()">Login</button>
        </div>
  </div>
</template>

<script>
    export default {
        name: 'Login',
        data() {
            return {
                input: {
                    email: "",
                    password: ""
                }
            }
        },
        methods: {
            async login() {
                let url = "https://localhost:44368/api/account/login";
                try {
                    let response = await fetch(url, {
                    method: "POST",
                    body: JSON.stringify(this.input), // Assumes data is in an object called form
                    headers: new Headers({
                        "Content-Type": "application/json"
                    })
                });
                
                if (response.ok) {
                    let token = await response.json();
                    localStorage.setItem("token", token.jwt);
                    
                } else {
                    alert("Server returned: " + response.statusText);
                }
                } catch (err) {
                 alert("Error: " + err);
                }
                return;
             
            }
        }
    }
</script>