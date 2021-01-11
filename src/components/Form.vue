<template>
  <form @submit.prevent="submitForm">
      <label>Email</label>
      <input type='email' required v-model="email"/>

      <label>Password</label>
      <input type='password' required v-model="password"/>
      <div v-if="passwordLength" class="error">{{passwordLength}}</div>

      <label>Role</label>
      <select v-model="role">
          <option value="developer">Web Developer</option>
          <option value="designer">Web Designer</option>
      </select>

      <label>Skills (tap Space to add the skill)</label>
      <input type='text'  v-model="tempskill" @keypress="addSkill"/>
       <div v-for="skill in skills" :key='skill' class='skills' @click='removeSkill(skill)'>
           <p>{{skill}}</p>
       </div>
      <div class='terms'>
          <input type='checkbox' required v-model="terms"/>
          <label>Accept terms and conditions</label>
      </div>

      <div class="submit">
          <button>Create an account</button>
      </div>

  </form>
  <Modal v-if="showmodal" @close='closeModal'/>
<p>Email : {{email}}</p>
<p>Password : {{password}}</p>
<p>role : {{role}}</p>
<p>terms accepted : {{terms}}</p>
</template>

<script>
import Modal from './Modal'
export default {
components:{
    Modal
},
 data(){
     return({
         email:'',
         password:'',
         role:'designer',
         terms:false,
         tempskill:'',
         skills:[],
         showmodal: false,
         passwordLength:''
     })
 },
 methods:{
     addSkill(e){
        if(!this.skills.includes(this.tempskill)){
           if(e.code === 'Space' && this.tempskill !=' '){
               this.skills.push(this.tempskill)
               this.tempskill=''
         }
        }else{
               this.showmodal= true
        }
     },
     closeModal(){
         this.showmodal= false
     },
     removeSkill(removedSkill){
        this.skills =  this.skills.filter(skill =>  skill !== removedSkill)
     },
     submitForm(){
         this.passwordLength = this.password.length > 5 ? '' : 'Password should have more than 5 characters'
         console.log('form submitted')
     }
 }
}
</script>

<style>
form{
    max-width: 400px;
    text-align: left;
    border-radius: 10px;
    padding: 40px;
    margin: 30px auto;
    background-color: white;

}
label{
    display: inline-block;
    margin: 25px 0 15px;
    color: #aaa;
    font-size: 0.6rem;
    letter-spacing: 1px;
    text-transform: uppercase;
    font-weight: bold;
    
}
input, select {
    display: block;
    padding: 10px 6px;
    width: 100%;
    box-sizing: border-box;
    border:none;
    border-bottom: 1px solid #ddd;
    color: #555;
}
input:focus , select:focus{

    border:none;
    border-bottom: 1px solid #ddd;
    color: #555;
    outline: 1px solid rgb(94, 94, 94);
}
input[type='checkbox']{
    display: inline-block;
    width: 30px;
    margin: 0 10px 0 0;
    position: relative;
    top:2px;
    outline: none;
}

.skills{
    display: inline-block;
    margin: 5px 5px 15px;
    color: rgb(71, 71, 71);
    font-size: 0.6rem;
    letter-spacing: 1px;
    text-transform: uppercase;
    font-weight: bold;
    background-color: #eee;
    border-radius: 20px;
    cursor: pointer;
    padding: 2px 10px;
}
button{
    background-color: rgb(16, 92, 235);
    margin: 1px auto;
    padding: 10px 30px ;
    color: #ffff;
    font-size: 0.7rem;
    letter-spacing: 1px;
    font-weight: bold;
    border: none;
    border-radius: 20px;
    cursor: pointer;
}
.button:focus{
    border:none;
    outline: none;
}
.submit{
    text-align: center;
}
.error{
    color: rgb(196, 2, 2);
    font-size: 0.8rem;
    font-weight: bold;
}
</style>