<template>
<div class="container">
    <form class="container-form" @submit="checkForm" action="#" method="#">
<div class="alert-error"  v-if="errors.length">
<p class=error-title>Пожалуйста исправьте указанные ошибки:</p>
<ul>
<li v-for="error in errors" :key="error">{{ error }}</li>
</ul>
<button class="button-error"  type="button" v-on:click="emptyArray">ok</button>
</div>
<div class="input-container">
  <input class="item-name" type="text" v-model="name" placeholder="имя*" />
  <input class="item-surname" type="text" v-model="surname" placeholder="фамилия*" />
  <input class="item-patronymic" type="text" v-model="patronymic" placeholder="отчество" />
<div class="befory-date">
  <input class="item-birthday" type="date" v-model="birthday" placeholder="дата родждения*" />
</div>
  <input class="item-numberMobil" type="number" maxlength="11" mixlength="11" v-model="numberMobil" placeholder="номер телефона* " />
</div>
<div class="container-menWomen">
<div class="item-men">
  <input  type="radio" id="men" value="men" v-model="picked" checked />
  <label for="men">men</label></div>
<div class="item-women">
  <input type="radio" id="women" value="women" v-model="picked" />
  <label for="women">women</label>
</div>
</div>
<div class="item-checked">
  <input type="checkbox" id="checkbox" v-model="checked" />
  <label for="checkbox" class="label-checkbox"> Не отправлять смс</label>
</div>
<div class="item-selected">
  <span class="selected-title"> Лечащий врач* </span>
    <select v-model="selected" >
      <option disabled value=""></option>
      <option> Иванов </option>
      <option> Захаров </option>
      <option> Чернышева</option>
    </select>
</div>
<div class= "item-multipleSelected">
  <span class="multipleSelected-title"> Группа клиентов* </span>
    <select v-model="multipleSelected" >
      <option disabled value=""></option>
      <option>VIP </option>
      <option>Проблемные</option>
      <option>ОМС</option>
    </select>
</div>
<span class="address-title"> Адрес: </span>
<div class="item-address">
    <input type="number" v-model="index" placeholder="Индекс"/>
    <input type="text" v-model="country" placeholder="Страна"/>
    <input type="text" v-model="region" placeholder="Область"/>
    <input type="text" v-model="city" placeholder="Город*"/>
    <input type="text" v-model="street" placeholder="Улица"/>
    <input type="text" v-model="home" placeholder="Дом"/>
</div>
<div class="item-selectedDocs">
    <span> Тип документа*</span>
      <select v-model="selectedDocs ">
        <option >паспорт</option>
        <option>Свидетельство о рождении</option>
        <option> Водительское удостоверение </option>
      </select>
</div>
<div class="item-selectedDocs_items">
  <input type="number" max="2" v-model="seriesDocs" placeholder="Серия"/>
  <input type="number" v-model="numberDocs" placeholder="Номер"/>
  <input type="text" v-model="issuedByDocs" placeholder="Кем выдан"/>
  <div class="befory-date">
    <input type="date" v-model="dateIssueDocs" placeholder="Дата выдачи*"/>
  </div>
</div>
<p class="item-required">* Поле обязательное для заполнения </p>
<button class="item-submit" type="submit" >Отправить</button>
</form>
  </div>
</template>

<script>
export default {
  name: 'FormRegistration',
  data() {
return {
errors: [],
name: '',
surname:'',
patronymic:'',
birthday: '',
numberMobil:'',
picked :'',
checked: false,
selected: '',
multipleSelected: '',
index:'',
country:'',
region:'',
city:'',
street:'',
home:'',
selectedDocs:'',
seriesDocs:'',
numberDocs:'',
issuedByDocs:'',
dateIssueDocs:'',
}
},
methods: {
checkForm: function (e) {
e.preventDefault();
let firstElement= String(this.numberMobil).split('') ;
let date=new Date();
let yearBirth;
let monthBirth;
let dayhBirth;
this.errors = [];

  if(!this.name) {
  this.errors.push('Требуется указать имя.');
}else{
  if (this.name.match(/\d/gi)) {
  this.errors.push('Требуется ввести только буквы в имени.');
}
}
  if(!this.surname) {
  this.errors.push('Требуется указать фамилию.');
}else{
  if (this.surname.match(/\d/gi)) {
  this.errors.push('Требуется ввести только буквы в фамилии.');
}
}

if (!this.birthday) {
  this.errors.push('Требуется указать дату рождения.');
}else{

  yearBirth = this.birthday.match(/\d/gi).slice(0, 4).join('');
  monthBirth =  this.birthday.match(/\d/gi).slice(4, 6).join('');
  dayhBirth =  this.birthday.match(/\d/gi).slice(6, 8).join('');

  if(date.getFullYear()-18 <Number(yearBirth)){
  this.errors.push('Требуется указать год рождения в диапазоне 1922 - 2004.');
}else{
  if(date.getMonth()+1 <Number(monthBirth)){
  this.errors.push('Требуется указать месяц рождения не позднее сегоднешнего.');
}else{
  if(date.getDate() <Number(dayhBirth)){
  this.errors.push('Требуется указать день рождения не позднее сегоднешнего.');
}}}}

  if(!this.numberMobil) {
  this.errors.push('Требуется указать номер телефона.');
}else {
  if(firstElement.length<11){
  this.errors.push('Требуется ввести 11 цифр номера телефона.');
}else{
  if(!firstElement[0].includes("7")){
  this.errors.push('Требуется ввести номер телефона в формате 79XXXXXXXXX.');
}}}

if ( !this.multipleSelected) {
  this.errors.push('Требуется указать свойство в категории Группа клиентов.');
}
if ( !this.selected) {
  this.errors.push('Требуется указать свойство в категории Лечащий врач.');
}
if (!this.city) {
  this.errors.push('Требуется указать город.');
}else{
  if(this.city.match(/\d/gi)){
  this.errors.push('Требуется ввести только буквы в названии города.');
}}

if (!this.selectedDocs) {
  this.errors.push('Требуется указать тип документа.');
}
if (!this.dateIssueDocs) {
  this.errors.push('Требуется указать дату выдачи документа.');
}
scroll(0, 0);
if (this.name &&
 this.surname &&
  this.surname &&
   this.city &&
    this.birthday &&
     this.numberMobil &&
      this.selected &&
       this.multipleSelected && 
        !this.name.match(/\d/gi) &&
         !this.surname.match(/\d/gi) &&
           !this.city.match(/\d/gi) &&
            firstElement[0].includes("7") &&
            firstElement.length>=11 &&
          date.getFullYear()-18 >=Number(yearBirth) &&
        date.getMonth()+1>= Number(monthBirth) &&
      date.getDate()>= Number(dayhBirth)
) 
{ 
alert( "Данные успешно сохранены");
return true;
}},
emptyArray: function(){
  this.errors.splice(0);
}}}
</script>

<style scoped lang="sass">
input,select
  height: 30px
  width: 100%
  border: none
  outline-style: none
  background-color: rgba(230, 230, 250, 0.7 )
  color: black
  padding-left: 5px
  margin-bottom: 5px
  &:focus
    border-bottom: white solid 1px

label
  font-size: 17px
  padding-top: 5px
span
  line-height: 30px
  vertical-align: bottom
  font-size: 17px
input[type="checkbox"]
  height: 25px
li
  line-height: 30px
  color: red
  font-size: 15px
  list-style: inside
.container
  margin:
    top: 5%
    bottom: 5%
  padding:
    left: 5%
    right: 5%
  max-width: 600px
  height: 100%
.container-form
  display: grid
  grid-template-columns: 3% 94% 3%
  grid-template-rows: 20px 175px 35px minmax(35px, auto) minmax(35px, auto) minmax(35px, auto) 32px auto 65px 140px
  background-color: rgba(230, 230, 250, 0.5 )
  border-radius: 20px
  padding-bottom: 20px
  position: relative
.alert-error
  max-width: 600px
  height: auto
  position: absolute
  z-index: 1
  background-color: rgba(224, 255, 255, 0.9 ) 
  border-radius: 20px
  padding: 20px
  top: 3%
  left: 5%
  right: 5%
.error-title
  font-size: 18px
  color: black
.button-error
  width: 80px
  height: 30px
  color: black
  border: none
  outline-style: none
  cursor: pointer
  box-shadow: 2px 3px 4px -2px black
  border-radius: 5px
.input-container
  display: flex
  flex-wrap: wrap
  grid-row: 2/3
  grid-column: 2/3 
.container-menWomen
  grid-row: 3/4
  grid-column: 2/3
  display: flex
  justify-content: space-between
.item-men
  height: 30px
  display: flex
#men
  margin-right: 10px
  width: 20px
.item-women
  height: 30px
  display: flex
#women
  margin-right: 10px
  width: 20px
.item-checked
  grid-row: 4/5
  grid-column: 2/3
  display: flex
#checkbox
  width: 20px
  margin-right: 10px
.label-checkbox
  display: inline
  vertical-align: bottom
.item-selected
  grid-row: 5/6
  grid-column: 2/3
  height: auto

.item-multipleSelected
  grid-row: 6/7
  grid-column: 2/3
  height: auto

.address-title
  grid-row: 7/8
  grid-column: 2/3
.item-address
  grid-row: 8/9
  grid-column: 2/3
  height: auto
  display: flex
  flex-wrap: wrap
  justify-content: space-around
  
.item-selectedDocs
  grid-row: 9/10
  grid-column: 2/3
  height: auto

.item-selectedDocs_items
  grid-row: 10/11
  grid-column: 2/3
  height: auto
  display: flex
  flex-wrap: wrap

.item-required
  grid-row: 11/12
  grid-column: 2/3
  height: auto
  padding:
    bottom: 10px
    top: 5px
.befory-date
  width: 100%
  height: auto
  display: flex
  position: relative
  &::after
    content: "*"
    color: #333
    font-size: 99%
    position: absolute
    top: 5px
    left: 82px
.item-submit
  grid-row: 12/13
  grid-column: 2/3
  height: 30px
  width: 100px
  cursor: pointer
  color: #2c3e50
  background-color: rgba(230, 230, 250, 0.7 )
  border: none
  outline-style: none
  box-shadow: 2px 3px 4px -2px black
  &:active
    background-color: white
</style>
