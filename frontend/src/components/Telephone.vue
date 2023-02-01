<template>

  <div class='telephoneBox'>
    <p class='flagImageBox' v-on:click='toogleActiveListOfCountries'>
      <img v-bind:src='

        require(

          "@/assets/flagsOfCounties/" + listOfCountries[Number(IndexOfSelectedCountry)].nameOfCountry + ".png"

        )'

      >
      <span class='arrow' v-html='arrow'></span>
    </p>
    <input type='text' v-on:keydown='format' v-model='FormatedTelephoneNumber'>
  </div>

<ul class='select' v-if='IsActiveListOfCountries'>
  <li 

  class='option'

  v-for='(country,index) in listOfCountries'

  v-on:click='selectCountry(index)'

  v-bind:style='styleObjectOfSelectedCountry(index)'>
    <p class='nameOfCountry'>{{country.nameOfCountry}}</p> 
    <p class='telephoneMask'>{{country.telephoneMask}}</p>
  </li>
</ul>
</template>

<script>
export default {

  data(){
    return{

      IndexOfSelectedCountry:'0',

      listOfCountries:[

    {nameOfCountry:'Russia', telephoneCode:'7', formatedTelephoneNumber:'*-***-**-**-***'},
    {nameOfCountry:'England', telephoneCode:'44', formatedTelephoneNumber:'**-***-****-****'},
    {nameOfCountry:'Spain', telephoneCode:'34', formatedTelephoneNumber:'**-***-***-***'},
    {nameOfCountry:'Italy', telephoneCode:'39', formatedTelephoneNumber:'**-**-***-***'},
    {nameOfCountry:'Germany', telephoneCode:'49', formatedTelephoneNumber:'**-***-****-****'},
    {nameOfCountry:'China', telephoneCode:'86', formatedTelephoneNumber:'**-***-***-****'},
    {nameOfCountry:'Japan', telephoneCode:'81', formatedTelephoneNumber:'**-***-**-****'},
    {nameOfCountry:'India', telephoneCode:'91', formatedTelephoneNumber:'**-****-******'},
    {nameOfCountry:'Kazakhstan', telephoneCode:'7', formatedTelephoneNumber:'*-***-**-*****'},

      ],

      IsActiveListOfCountries:false,

      arrow:'&#9660;',

      FormatedTelephoneNumber:'+7-***-**-**-***',

      mask:'+*-***-***-**-**',

    }

  },

  methods:{

    setFormat(value, dataFormat, mask){
      // удаляем все нечисловые значения из полученной строки
      const clearedString=value.replace(/[^0-9]/g, "");

      // преобразуем строку в массив символов
      const chars = clearedString.split('');

      let count=0;

      let formattedString='';

      //форматируем строку
      for(let i = 0; i < dataFormat.length; i++){
        const char = dataFormat[i];
        if (chars[count]){

          if (/\*/.test(char)){
            formattedString += chars[count];
            count++;

          }else{
            formattedString += char;
          }
        }
            else if(mask){

              const splittedMask = mask.split('');
              if (splittedMask[i]){
                formattedString += splittedMask[i];
              }
            }
      }

      return formattedString;

    },

    format(event){

      //Отменяем события нажатия клавиши
      event.preventDefault();

      //Проверяем, что введенный символ является числом - удаляем из символа все символы,
      //которые не являются цифрами, и если длина символа больше нуля, то он является числом
      if(event.key.replace(/[^0-9]/g, "").length>0){

        //Убираем маску в строке и проверяем, что в ней еще есть место для ввода цифр
        if(

            this.FormatedTelephoneNumber.replace(/[^0-9]/g, "").length
              <
            this.FormatedTelephoneNumber.replace(/-/g, "").length-1
          ){

          //Получаем отформатированную строку с датой рождения
          this.FormatedTelephoneNumber=this.setFormat(

            this.FormatedTelephoneNumber.replace(/[^0-9]/g, "")+event.key,

            this.mask,

            this.mask,

            );
        }

    }

    //Проверяем, является ли введенный символ символом удаления и что длина
    //строки без маски больше нуля - в ней есть цифры
    //
    if(

      event.key=='Backspace' && this.FormatedTelephoneNumber.replace(/[^0-9]/g, "").length

      >this.listOfCountries[Number(this.IndexOfSelectedCountry)].telephoneCode.length
      ){

      //Получаем все числа в дате
      let string =this.FormatedTelephoneNumber.replace(/[^0-9]/g, "");
      //Получаем длину строки даты
      let length = this.FormatedTelephoneNumber.replace(/[^0-9]/g, "").length;
      //Получаем подстроку с нулевого символа до предпоследнего
      let trimmedString = string.substring(0, length-1);

      //Получаем отформатированную строку с датой рождения
      this.FormatedTelephoneNumber=this.setFormat(

        trimmedString,

            this.mask,

            this.mask,

        );

      }

    },

    toogleActiveListOfCountries(){

      if(this.IsActiveListOfCountries==false){//Если стрелка равна стрелке вниз, то 

        this.arrow='&#9650;';//Показываем стрелку вверх
        this.IsActiveListOfCountries=true;//Открываем список стран
      
      }else if(this.IsActiveListOfCountries==true){

        this.arrow='&#9660;';//Показываем стрелку вниз
        this.IsActiveListOfCountries=false;//Закрываем список стран

      }

    },

    styleObjectOfSelectedCountry(index){

      let style={};



      if(String(index)==this.IndexOfSelectedCountry){

        style={ background: 'rgb(30, 144, 255)', color: 'white'};

      }

      return style;

    },

    selectCountry(index){

      this.IndexOfSelectedCountry=index;

      this.toogleActiveListOfCountries();

      //Получаем новую маску
      this.mask='+' + this.listOfCountries[Number(index)].formatedTelephoneNumber;

      this.FormatedTelephoneNumber=

      '+' + this.listOfCountries[Number(index)].telephoneCode +

      this.listOfCountries[Number(index)].formatedTelephoneNumber.substring(this.listOfCountries[Number(index)].telephoneCode.length);

    },




  },

}
</script>






<style scoped>


  .telephoneBox{

    margin-top:5px;
    height:50px;
    max-width:350px;
    width:70%;
    display:flex;
    justify-content:flex-start;
    align-items:center;
    padding-left:5px;
    font-size:20px;
    border-style:solid;
    border-color:#cdd6f3;;
    border-width:1px;
    border-radius: 8px;

  }

  .flagImageBox{

    position:relative;

    height:100%;
    width:40px;
    display:flex;
    align-items:center;
    justify-content:center;
    cursor:pointer;
    user-select:none;
  }


  .arrow{

    position:absolute;
    right:2px;
    margin:auto;
    font-size:10px;
    width:6px;

  }

  .flagImageBox>img{

    height:30px;
    width:auto;

  }
  
  .telephoneBox>input{

    margin-left:10px;
    margin-right:5px;
    height:30px;
    width:80%;
    padding-left:5px;
    font-size:18px;

    border-style:solid;
    border-color:#cdd6f3;;
    border-width:1px;
    border-radius: 8px;
    padding-left:10px;
  }


  .select{

    border-style:solid;
    border-color:#cdd6f3;;
    border-width:1px;
    border-radius: 8px;
    margin-top:5px;
    height:100px;
    max-width:350px;
    width:70%;
    overflow:auto;


  }

  .option{

    height:25px;
    width:100%;
    cursor:pointer;
    display:flex;
    align-items:center;
    justify-content:flex-start;
    padding-left:10px;
    font-size:15px;

  }

  .option:hover{

    background-color: rgba(192, 192, 192, 0.7);
    
  }

  .nameOfCountry{

    margin-right:5px;
  }


</style>
