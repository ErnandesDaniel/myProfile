<template>

  <div class="block">

    <div class='currentPassword'>Текущий пароль: {{ currentPassword }}</div>


    <span>Введите новый пароль</span>
    <input type='text' v-model='newPassword'>

    <span>Подтвердите новый пароль</span>
    <input type='text' v-model='confirmationNewPassword'>


    <input type='button' value='Сменить пароль' v-on:click='changePassword'>
    <div v-show='errorExist' class='error'>{{ errorMessage }}</div>

  </div>

</template>

<script>
export default {

  data(){
    return{

      currentPassword:'fjl;safji^&op78',
      newPassword:'',
      confirmationNewPassword:'',
      errorMessage:'',
      errorExist:false,

    }
  },


  watch:{

    newPassword(){this.errorExist=false;},

    confirmationNewPassword(){this.errorExist=false;},

  },


  methods:{

    changePassword(){

     if(this.newPassword.length<8){

          this.errorMessage='Минимальная длина пароля 8 символов';

          this.errorExist=true;

      }

      if(this.newPassword!=this.confirmationNewPassword && this.errorExist==false){

          this.errorMessage='Пароли должны совпадать';

          this.errorExist=true;

      }

      if(this.errorExist==false){

        this.currentPassword=this.newPassword;

        this.newPassword='';
        this.confirmationNewPassword='';

      }

    }
  },

}
</script>


<style scoped>

  .currentPassword{

    font-size:20px;
    max-width:350px;
    width:70%;

  }

  .error{

    color:red;
    margin-top:20px;
    width:80%;
    max-width:350px;
    text-align:center;
    font-size:20px
  }


  input[type='text'],input[type='button']{

    margin-top:5px;
    height:50px;
    max-width:350px;
    width:70%;
    display:flex;
    justify-content:center;
    align-items:center;
    padding-left:5px;
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
