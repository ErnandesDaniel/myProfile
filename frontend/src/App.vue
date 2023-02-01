<template>

  <ChangingAvatar/>
  <PersonalInformation/>
  <ChangingPassword/>


</template>

<script>

import ChangingAvatar from './components/ChangingAvatar.vue'
import ChangingPassword from './components/ChangingPassword.vue'
import PersonalInformation from './components/PersonalInformation.vue'

export default {

  components: {
    ChangingAvatar,
    ChangingPassword,
    PersonalInformation,
  }
}
</script>

<style>

  .block{
    display:flex;
    flex-direction:column;
    align-items:center;
    padding-top:20px;
    width:100%;
  }

  #app{

    padding-bottom:80px;

  }

  span{

    margin-top:15px;
    display:block;
    color:black;
    max-width:350px;
    width:70%;
    padding-left:5px;
    font-size:15px;

  }



</style>
