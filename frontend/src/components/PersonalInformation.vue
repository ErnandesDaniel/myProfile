<template>
  <div class="block">

    <span>Введите ФИО</span>
    <input type='text' v-model='fullName'>


    <DateOfBirthday/>


    <span>Введите Email</span>
    <input type='text' v-model='email'>


    <span>Введите город</span>
    <input type='text' v-model='city'>

    <span>Введите номер телефона</span>
    <Telephone/>

    <span>Выберите языки, которыми владеете</span>
    <SelectLanguages/>


    <input type='button' value='Сохранить данные' v-on:click='savePersonalInformation'>
    <div v-show='errorExist' class='error'>{{ errorMessage }}</div>

  </div>
</template>

<script>

import SelectLanguages from './SelectLanguages.vue'
import DateOfBirthday from './DateOfBirthday.vue'
import Telephone from './Telephone.vue'

export default {

  components:{

    SelectLanguages,
    DateOfBirthday,
    Telephone,

  },

  data(){
    return{

      fullName:'Илон Маск',
      email:'elon_musk@gmail.com',
      city:'Tехасс',
      errorMessage:'',
      errorExist:false,

    }
  },


  watch:{

    fullName(){this.errorExist=false;},

    email(){this.errorExist=false;},

  },


  methods:{

    savePersonalInformation(){

      if(this.fullName.length<1){

        this.errorExist=true;
        this.errorMessage='Введите имя';

      }


      if(!this.validateEmail(this.email)){

        this.errorExist=true;
        this.errorMessage='Невалидный email';

      }


      if(this.errorExist==false){

        alert('Данные сохранены!');

      }
    },

    validateEmail(email){
      return String(email)
        .toLowerCase()
        .match(
          /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/
        );
    },



  },

}
</script>

<style scoped>

  div{

    font-size:20px;

  }

  .error{

    color:red;
    margin-top:20px;
    width:80%;
    max-width:350px;
    text-align:center;
    font-size:20px
  }



  input[type='text'], input[type='button']{

    margin-top:5px;
    height:50px;
    max-width:350px;
    width:70%;
    display:flex;
    justify-content:center;
    align-items:center;
    padding-left:10px;
    font-size:20px;
    border-style:solid;
    border-color:#cdd6f3;;
    border-width:1px;
    border-radius: 8px;

  }


  input[type='button']{
    cursor:pointer;
  }


  @media(max-width: 370px){

    input,div{
      font-size:16px;

    }

  }

</style>
