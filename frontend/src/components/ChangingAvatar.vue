<template>

  <div class="block">

    <img v-bind:src='photo'/>

    <div class='changeButtons'>
        <div class='button' v-on:click='deleteAvatar'>Удалить аватар</div>
        <label for='fileElem' class='button'>Изменить аватар</label>

        <input 

          ref='file'
          type="file" 
          style="display:none" 
          v-on:change='cnangeAvatar()' 
          id="fileElem"

        />

    </div>

  </div>

</template>

<script>
export default {

  data(){
    return{

      photo:require("@/assets/avatar.png"),

    }
  },

  methods:{

     cnangeAvatar(){

      //Получаем данные из файла в виде объекта blod
      let file = this.$refs.file.files[0];

      console.log(file);

      if(

        file.type=='image/png' ||

        file.type=='image/jpeg' ||

        file.type=='image/jpg'

      ){

        //Создаем на основе blob объекта URL и изменяем аватар
        this.photo=URL.createObjectURL(file);

      }

    },

    deleteAvatar(){

      this.photo=require("@/assets/defaultAvatar.png");

    },
  }

}
</script>


<style scoped>

img{
  height:auto;
  width:50%;
  max-width:300px;
  border-radius:100%;
  pointer-events:none;
  user-select:none;

}

.changeButtons{
  display:flex;
  margin-top:20px;
  justify-content:space-between;
  width:360px;
}

.button{
  display:flex;
  justify-content:center;
  align-items:center;
  width:160px;
  height:30px;
  font-size:20px;
}

.button:hover{
  cursor:pointer;
  font-weight:bold;
}

@media(max-width: 370px){

  .changeButtons{
    display:flex;
    align-items:center;
    flex-direction:column;
    width:90%;
  }


  .button{
    font-size:18px;
    margin-top:10px;
  }


}

</style>
