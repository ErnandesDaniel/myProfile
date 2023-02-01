<template>

    <div class='areaOfSelectedLanguages'>

      <p class='selectedLanguage' v-for='(languages,index) in ListOfselectedLanguages'>
        {{languages}}
        <span class='removeSelectedLanguage' v-on:click='removeSelectedLanguage(index)'>&#215;</span>
      </p>

      <div class='emptyListOfSelectedLanguages' v-show='ListOfselectedLanguages.length==0'>Выбранные языки</div>

    </div>

    <select

      multiple="multiple" 
      v-model='ListOfselectedLanguages'
      >
        <option :value="languages" v-for='languages in listOfAllLanguages'>{{languages}}</option>
    </select>
</template>




<script>
export default {

  data(){
    return{

      ListOfselectedLanguages:[],

      listOfAllLanguages:[
        'English', 
        'Russian', 
        'Spanish', 
        'Italian',
        'German',
        'Chinese',
        'Japanese', 
        'Kazakh',
        'Indian',
      ],
    }
  },

  methods:{

  selectLanguages(event){

    console.log(event);

  },

    removeSelectedLanguage(index){

      this.ListOfselectedLanguages.splice(index, 1);

    }
  },

}
</script>


<style scoped>

  .areaOfSelectedLanguages{

    margin-top:5px;
    padding:5px;
    display:flex;
    flex-wrap:wrap;
    justify-content:flex-start;

    min-height:50px;
    max-width:350px;
    width:70%;
    border-style:solid;
    border-color:#cdd6f3;;
    border-width:1px;
    border-radius: 8px;

  }

  .emptyListOfSelectedLanguages{

    flex-basis:100%;
    display:flex;
    height:50px;
    justify-content:center;
    align-items:center;
    font-size:20px;


  }


  .selectedLanguage{

    position:relative;
    min-width:50px;
    height:40px;
    margin-right:5px;
    margin-left:5px;

    margin-top:5px;
    margin-bottom:5px;


    background-color: rgba(192, 192, 192, 0.7);

    border-radius:10px;
    padding-left:5px;
    padding-right:5px;

    display:flex;
    align-items:center;
    justify-content:center;
    user-select:none;

    padding-right:20px;

  }

  .removeSelectedLanguage{

    position:absolute;
    right:10px;
    top:0px;
    font-size:25px;
    height:10px;
    width:5px;
    display:flex;
    align-items:center;
    justify-content:center;
    cursor:pointer;

  }


  select{

    border-style:solid;
    border-color:#cdd6f3;;
    border-width:1px;
    border-radius: 8px;
    margin-top:5px;
    height:100px;
    max-width:350px;
    width:70%;

  }

  option{

      height:25px;
      width:100%;
      padding-left:5px;
      padding-top:5px;
      cursor:pointer;

  }

  option:hover{

    background-color: rgba(192, 192, 192, 0.7);
    
  }

</style>
