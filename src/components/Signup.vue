<template>
  <form action="" @submit.prevent="submit">
      <label for="" >Email</label>
      <input type="email" required v-model="email">

      <label for="">Password</label>
      <input type="password" v-model="password">
      <p class="errorMsg" v-if="errorMsg">{{errorMsg}}</p>

      <label for="">Roles:</label>
      <select v-model="role">
          <option value="developer">Web Developer</option>
          <option value="designer">Web Designer</option>
      </select>

      <div>
          <label for="">Skills</label>
          <input type="text" @keyup.alt="addSkill" v-model="skill">
      </div>

      <div v-for="skill in skills" :key="skill">
         <p>{{skill}} <span class="cross" @click="deleteSkill(skill)">&#x2718;</span></p> 
      </div>
    <!-- Single Checkbox -->
      <div>
          <input type="checkbox" v-model="accept">
          <label for="">Accept Terms and Conditions</label>
      </div>

      <div class="align">
          <button class="create">Create Account</button>
      </div>

      <!-- Multiple checkbox -->
      <!-- <label for="">Check Name</label><br>
      <div>
       <input type="checkbox" value="Aung Aung" v-model="name" >
       <label for="">Aung Aung</label><br>

       <input type="checkbox" value="Mg Mg" v-model="name"  >
       <label for="">Mg Mg</label><br>

       <input type="checkbox" value="Ko Ko " v-model="name" >
       <label for="">Ko KO</label><br>

       <input type="checkbox" value="Chit" v-model="name" >
       <label for="">Chit</label>

      </div> -->
       
  </form>

  <p>email - {{email}}</p>
  <p>password - {{password}}</p>
  <p>role - {{role}}</p>
  <p>accept - {{accept}}</p>
  <!-- <p>names - {{name}}</p> -->
 
</template>

<script>
export default {
    data(){
        return{
            email:"aung@gmail.com",
            password:"",
            role:"",
            accept:false,
            // name:[],
            skills:[],
            skill:"",
            errorMsg:"",
        }
    },
    methods:{
        addSkill(e){
            if(e.key==="," && this.skill){
                this.skills.push(this.skill);
                this.skill="";
            }
        },
        deleteSkill(skill){
            this.skills=this.skills.filter(loopSkill => {
                return loopSkill != skill ;
            })
        },
        submit(){
            if(this.password.length<8){
                this.errorMsg = " Password must be 8 characters."
            }
        }
    }   
}
</script>

<style>
    form{
        max-width: 420px;
        margin: 30px auto;
        background: white;
        text-align: left;
        padding: 40px;
        border-radius: 10px;
    }
    label{
        color: #aaa;
        display: inline-block;
        margin: 25px 0 15px;
        font-size: 0.6em;
        text-transform: uppercase;
        letter-spacing: 1px;
        font-weight: bold;
    }
    input,select{
        display: block;
        padding: 10px 6px;
        width: 100%;
        box-sizing: border-box;
        border: none;
        border-bottom: 1px solid #ddd;
        color: #555;
    }
    input[type="checkbox"]{
        display: inline-block;
        width: 16px;
        margin: 0 10px 0 0 ;
        position: relative;
        top: 2px;
    }
    .cross{
        cursor: pointer;
        color: red;
    }
    .create{
        background-color: royalblue;
        padding: 8px;
        color: white;
        border-radius: 10px;
    }
    .align{
        text-align: center;
    }
    .errorMsg{
        color : crimson;
    }
</style>