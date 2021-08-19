<template>

    <div>
        <div class="head">
            <button>APPLICATION FORM</button>
        </div>
  <!-- .prevent prevents the page from reloading after sunmitting, only shows in the console -->
  <form @submit.prevent="handleSubmit">
      <label>Email</label>
      <input type="email" required v-model="email">

       <label>Password</label>
      <input type="password" required v-model="password">
      <div v-if="passwordError" class="error">{{ passwordError}}</div>

      <label>Role:</label>
      <select v-model="role">
          <option value="developer">Web Developer</option>
          <option value="designer">Web designer</option>
      </select>

        <label>Skills</label>
        <input type="text" v-model="tempSkill" @keyup.alt="addSkill">
        <!-- you could also use keypress or keydown -->
        <div v-for="skill in skills" :key="skill" class="pill">
            <span @click="deleteSkill(skill)">{{ skill }}</span>
            <!-- always have a key property whenever you use the v-for directive -->
        </div>


        <div class="terms">
            <input type="checkbox" v-model="terms" required>
            <!-- required means that the box has to be checked -->
            <label>Accept terms and conditions</label>
        </div>

        <!-- this below is for multiple checkboxes, you dont need to say required cos the user doesnt need to check all the boxes. you also need to add 'value' when working with multiple checkboxes to make each distinct  -->
        <!-- <div>
            <input type="checkbox" value="paul" v-model="names">
            <label>Paul</label>
        </div>
        <div>
            <input type="checkbox" value="king" v-model="names">
            <label>KING</label>
        </div>
        <div>
            <input type="checkbox" value="yochabel" v-model="names">
            <label>Yochabel</label>
        </div> -->

        <div class="submit">
            <button>Submit</button>
        </div> 

        <footer class="footer">designed by paulking</footer>
  </form>
<div class="output">
       <p>Email: {{email}}</p>
       <p>Password: {{password}}</p>
       <p>Role: {{ role }}</p>
       <p>Terms accepted: {{ terms }}</p>
       <!-- <p>Names: {{names}}</p> -->
</div>
</div>
</template>

<script>
export default {
 name: 'SignupForm',

 data() {
     return {
         email: 'mario',
         password: '',
         role: 'designer',
         terms: false,
         names: [],
         tempSkill: [],
         skills: [],
         passwordError: ''
     }
 },
 methods: {
     addSkill(e) {
        //  e = event object
        if (e.key === ',' && this.tempSkill) {
            if (!this.skills.includes(this.tempSkill )) {
                this.skills.push(this.tempSkill)
            }
            this.tempSkill = ''
        }
     },

     deleteSkill(skill) {
         this.skills = this.skills.filter((item) => {
             return skill !== item
         })
         },

    handleSubmit() {
        // validate password
       this.passwordError = this.password.length > 5 ? '' : 'Password must be at least 6 characters long'

       if(!this.passwordError) {
           console.log('email: ', this.email)
           console.log('password: ', this.password)
           console.log('role: ', this.role)
           console.log('skills: ', this.skills)
           console.log('terms accepted: ', this.terms)
       }
    }
     }
 }
</script>

<style>
form {
    max-width: 420px;
    margin: 30px auto;
    background: white;
    text-align: left;
    padding: 40px;
    border-radius: 10px;
}
label {
    color: #aaa;
    display: inline-block;
    margin: 25px 0 15px;
    font-size: 0.6em;
    text-transform: uppercase;
    letter-spacing: 1px;
    font-weight: bold;
}
input, select {
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
    /* border-radius makes it rounded at the corners */
    font-size: 12px;
    letter-spacing: 1px;
    font-weight: bold;
    color: #777;
    cursor: pointer;
}
button {
    background: #0b6dff;
    border: 0;
    padding: 10px 20px;
    margin-top: 20px;
    color: white;
    border-radius: 10px;
    font-weight: bold;
}
.submit, .head {
    text-align: center;
}


.error {
    color: #ff0062;
    margin-top: 10px;
    font-size: 0.8em;
    font-weight: bold;
}

.output {
    text-align: center;
    /* font-display: inherit; */
    color: #0b6dff;
    font-weight: bold;
}

.footer {
    text-align: end;
    font-size: 10px;
    color: darkgray;
    margin-bottom: -20px;
}
</style>