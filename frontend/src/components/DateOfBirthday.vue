<template>


  <span>Введите дату рождения</span>

  <input type='date'

    v-model='selectedDate' 

    v-on:change='selectDateInCalendar'

    placeholder="Открыть календарь"

  >

  <input type='text' ref='text' v-model='FormatedDateOfBirthday' v-on:keydown='format'>

</template>

<script>

export default {


  data(){
    return{
      FormatedDateOfBirthday:'DD.MM.YYYY',
      selectedDate:'',

    }
  },

  methods:{

    selectDateInCalendar(){

      let arrayOfDate=this.selectedDate.split('-');
      let numberOfDate=arrayOfDate[2]+''+arrayOfDate[1]+''+arrayOfDate[0];

      //Устанавливаем дату в поле ввода даты с маской
      this.FormatedDateOfBirthday=this.setFormat(

        numberOfDate,

            '**.**.****',

            "MM.DD.YYYY"

        );

    },

    format(event){

      //Отменяем события нажатия клавиши
      event.preventDefault();

      //Проверяем, что введенный символ является числом - удаляем из символа все символы,
      //которые не являются цифрами, и если длина символа больше нуля, то он является числом
      if(event.key.replace(/[^0-9]/g, "").length>0){

        //Убираем маску в строке и проверяем, что в ней еще есть место для ввода цифр
        if(this.FormatedDateOfBirthday.replace(/[^0-9]/g, "").length<8){

          //Получаем отформатированную строку с датой рождения
          this.FormatedDateOfBirthday=this.setFormat(

            this.FormatedDateOfBirthday.replace(/[^0-9]/g, "")+event.key,

            '**.**.****',

            "MM.DD.YYYY"

            );
        }

    }

    //Проверяем, является ли введенный символ символом удаления и что длина
    //строки без маски больше нуля - в ней есть цифры
    //
    if(event.key=='Backspace' && this.FormatedDateOfBirthday.replace(/[^0-9]/g, "").length>0){

      //Получаем все числа в дате
      let string =this.FormatedDateOfBirthday.replace(/[^0-9]/g, "");
      //Получаем длину строки даты
      let length = this.FormatedDateOfBirthday.replace(/[^0-9]/g, "").length;
      //Получаем подстроку с нулевого символа до предпоследнего
      let trimmedString = string.substring(0, length-1);

      //Получаем отформатированную строку с датой рождения
      this.FormatedDateOfBirthday=this.setFormat(

        trimmedString,

            '**.**.****',

            "MM.DD.YYYY"

        );

      }

    },


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

    }

  },



mounted(){

}

}
</script>


<style scoped>

input[type="date"] {
  position: relative;
}

input[type="date"]::-webkit-calendar-picker-indicator {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  width: auto;
  height: auto;
  color: transparent;
  background: transparent;
  cursor:pointer;
}

input[type="date"]::-webkit-inner-spin-button,
input[type="date"]::-webkit-clear-button {
  z-index: -10;
}

input[type="date"]::-webkit-input-placeholder {
  z-index: 99;
}

input[type="date"]:placeholder {
  z-index: 99;
}
input[type="date"]:not(.has-value):before {
  content: attr(placeholder);
  width: 100%;
}

input[type="date"] {
  padding: 12px 20px;
}







  span{

    margin-top:10px;
    display:block;
    color:black;
    max-width:350px;
    width:70%;

  }

  input{

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
    border-color:#cdd6f3;
    border-width:1px;
    border-radius: 8px;

  }

</style>
