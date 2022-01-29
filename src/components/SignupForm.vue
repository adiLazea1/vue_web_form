<template>
    <form @submit.prevent="handleSubmit">
        <label>Email</label>
        <input type="email" v-model="email" required>
        <br>
        <label>Password</label>
        <input type="password" v-model="password" required>
        <div v-if="passwordError" class="error">{{passwordError}}</div>

        <label>Role</label>
        <select v-model="role">
            <option value="developer" >Web Developer</option>
            <option value="designer">Web Designer</option>
        </select>
        <br>

        <label >Skills:</label>
        <input type="text" v-model="tempSkill" @keyup.alt="addSkill" placeholder="ALT + , pt adaugare skill nou">
        <div v-for="skill in skills" :key="skill" class="pill">
            <span @click="deleteSkill(skill)">  {{ skill }}   </span>
        </div>
                
        <br>
        <label >Animal preferat</label>
        <div>
            <input type="checkbox" value="pisica" v-model="names">
            <label >pisica</label>
        </div>
        <div>
            <input type="checkbox" value="caine" v-model="names">
            <label >caine</label>
        </div>
        <div>
            <input type="checkbox" value="iepure" v-model="names">
            <label >iepure</label>
        </div>

        <br>

        <div class="terms">
            <input type="checkbox" v-model="terms" id="termsCheckbox" required >
            <label for="termsCheckbox"> Accept terms ad contidions</label>
        </div>
        <br>

        <div class="submit">
            <button>Create an Account</button>
        </div>

    </form>
  
    <p>Email: {{email}}</p>
    <p>Password: {{password}}</p>
    <p>Role: {{role}}</p>
    <p>Skills {{ skills }}</p>
    <p>Terms: {{ terms }} </p>
    <p>Name: {{ names }} </p>
</template>

<script>
export default {    
    data() {
        return {
            email: 'ion@ionescu.com',
            password: '',
            passwordError: '',
            role: 'designer',
            tempSkill: '',
            skills: [],
            terms: false,
            names: [],
        }
    },

    methods: {
        addSkill(e) {
            if(e.key === ',' && this.tempSkill) {
                if (!this.skills.includes(this.tempSkill)) {
                    this.skills.push(this.tempSkill);    
                }
                this.tempSkill = '';
            }
            console.log(e);
        },

        deleteSkill(skill) {
            this.skills = this.skills.filter((elem)=> { 
                return elem !== skill
                }); 
            console.log(skill);
        },

        handleSubmit() {
            // validate password
            this.passwordError = this.password.length > 5 ? '' : "Parola este prea scurta. Trebuie sa aiba minim 5 caractere."

            if (!this.passwordError) {
                console.log('email: ' + this.email);
                console.log('password: ' + this.passwordError);
                console.log('role: ' + this.role);
                console.log('skils: ' + this.skills);
                console.log('terms accepted: ' + 'this.terms');
                console.log('animale: ' + this.names);

            }

            console.log(this.passwordError);
            console.log('form submitted')
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
        font-size: .6em;
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
        margin: 0 10px 0;
        position: relative;
        top: 2px;
    }

    .pill {
        display: inline-block;
        margin: 20px 10px 0 0;
        padding: 6px 12px;
        border-radius: 20px;
        font-size: 12px;
        letter-spacing: 1px;
        color: #777;
        background: #eee;
        cursor: pointer;
    }

    button {
        background: #0b6dff;
        border: 0;
        padding: 10px 20px;
        margin-top: 20px;
        color: white;
        border-radius: 2px;
    }

    .submit {
        text-align: center;
    }

    .error {
        color: orangered;
        font-size: 12px;
        padding: 4px;
    }

</style>