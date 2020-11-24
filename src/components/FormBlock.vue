<template>
  <div class="form">
    <h2 class="form-title">Форма заполнения данных</h2>
    <form class="form-block" @submit.prevent="submitHandler">
        <div class="form-block__info form-block__info-left">
            <div class="form-user__logo">
                <img src="../assets/user.png" alt="user">
            </div>
            <div class="form-input__group">
                <div class="form-input__block" :class="{ 'form-group__error': $v.surname.$error }">
                    <label>Фамилия*</label>
                    <input 
                        id="surname"
                        class="form-input__person" 
                        type="text" 
                        name="surname" 
                        placeholder="Фамилия*"
                        v-model.trim="$v.surname.$model" 
                        :class="{invalid: ($v.surname.$dirty && !$v.surname.required)}" 
                    >
                    <small
                        class="form-helper__text invalid"
                        v-if="$v.surname.$dirty && !$v.surname.required"
                    >Поле Фамилия не должно быть пустым</small>
                    <small
                        class="form-helper__text invalid"
                        v-if="$v.surname.$dirty && !$v.surname.minLength"
                    >
                        Введите две или более буквы
                    </small>
                </div>
                <div class="form-input__block" :class="{ 'form-group__error': $v.name.$error }">
                    <label for="name">Имя*</label>
                    <input 
                        v-model.trim="$v.name.$model" 
                        :class="{invalid: ($v.name.$dirty && $v.name.required)}" 
                        class="form-input__person" 
                        type="text" 
                        name="name" 
                        placeholder="Имя*"
                    >
                    <small
                        class="form-helper__text invalid"
                        v-if="$v.name.$dirty && !$v.name.required"
                    >Поле Фамилия не должно быть пустым</small>
                    <small
                        class="form-helper__text invalid"
                        v-if="$v.name.$dirty && !$v.name.minLength"
                    >
                        Введите две или более буквы
                    </small>
                </div>
                <div class="form-input__block">
                    <label for="middleName">Отчество</label>
                    <input 
                        class="form-input__person" 
                        type="text" 
                        name="middleName" 
                        v-model.trim="$v.middleName.$model" 
                        placeholder="Отчество"
                    >
                </div>
            </div>
            <div class="form-input__group">
                <div class="form-input__block" :class="{ 'form-group__error': $v.birthday.$error }">
                    <label>Дата рождения*</label>
                    <input 
                        v-model.trim="$v.birthday.$model" 
                        :class="{invalid: ($v.birthday.$dirty && $v.birthday.required)}" 
                        class="form-input__person"  
                        type="date" 
                        placeholder="Дата рождения*"
                    >
                    <small
                        class="form-helper__text invalid"
                        v-if="$v.name.$dirty && !$v.name.required"
                    >
                        Укажите дату рождения
                    </small>
                </div>
                <div class="form-input__block" :class="{ 'form-group__error': $v.phone.$error }">
                    <label>Номер телефона*</label>
                    <input 
                        class="form-input__person" 
                        type="text" 
                        name="phone" 
                        id="phone"
                        placeholder="Номер телефона*"
                        v-model.trim="$v.phone.$model" 
                        :class="{invalid: ($v.phone.$dirty && $v.phone.required)}" 
                    >
                    <small
                        class="form-helper__text invalid"
                        v-if="$v.phone.$dirty && !$v.phone.required"
                    >
                        Укажите номер телефона
                    </small>
                    <small
                        class="form-helper__text invalid"
                        v-if="$v.phone.$dirty && !$v.phone.numeric"
                    >
                        Укажите цифры
                    </small>
                    <small
                        class="form-helper__text invalid"
                        v-if="$v.phone.$dirty && !$v.phone.minLength"
                    >
                        Укажите минимум 11 цифр
                    </small>
                </div>
            </div>
            <div class="form-input__group">
                <div class="form-input__block">
                    <label>Пол</label>
                    <select 
                        class="form-input__person" 
                        name="gender"
                        v-model.trim="$v.gender.$model" 
                    >
                        <option value="male">Мужской</option>
                        <option value="male">Женский</option>
                    </select>
                </div>
                <div class="form-input__block">
                    <label>Лечащий врач</label>
                    <select 
                        class="form-input__person" 
                        name="doctor"
                        v-model.trim="$v.doctor.$model" 
                    >
                        <option value="ivanov">Иванов</option>
                        <option value="zakharov">Захаров</option>
                        <option value="chernysheva">Чернышева</option>
                    </select>
                </div>
            </div>
            <div class="form-input__group form-group__inputs-last">
                <div class="form-input__block-checkbox">
                    <label for="sms">Не отправлять СМС</label>
                    <input 
                        type="checkbox" 
                        name="sms" 
                        id="sms"
                        v-model.trim="$v.smsMail.$model" 
                    >
                </div>
            </div>
            <div class="form-input__group">
                <div class="form-input__block form-input__block-multiselect" :class="{ 'form-group__error': $v.clients.$error }">
                    <label for="doctor">Группа клиентов*</label>
                    <multiselect 
                        class="form-input__multiselect"
                        v-model="clients" 
                        tag-placeholder="Add this as new tag" 
                        placeholder="Добавьте одно или несколько" 
                        label="name" 
                        track-by="code" 
                        :options="options" 
                        :multiple="true" 
                        :taggable="false" 
                        @tag="addTag">
                    </multiselect>
                    <small
                        class="form-helper__text invalid"
                        v-if="$v.clients.$dirty && !$v.clients.required"
                    >
                        Выберите одно или несколько
                    </small>
                </div>
            </div>
        </div>
        <div class="form-block__info form-block__info-right">
            <h3 class="form-block__info-title">Адрес:</h3>
            <div class="form-block__address"> 
                <div class="form-input__group">
                    <div class="form-input__block">
                        <label>Страна</label>
                        <input 
                            class="form-input__person form-input__address" 
                            type="text" 
                            name="country" 
                            placeholder="Страна"
                            v-model.trim="$v.country.$model" 
                        >
                    </div>
                    <div class="form-input__block">
                        <label>Область</label>
                        <input 
                            class="form-input__person form-input__address" 
                            type="text" 
                            name="region" 
                            placeholder="Область"
                            v-model.trim="$v.region.$model" 
                        >
                    </div>
                    <div class="form-input__block" :class="{ 'form-group__error': $v.city.$error }">
                        <label>Город*</label>
                        <input 
                            class="form-input__person form-input__address" 
                            type="text" 
                            name="city" 
                            placeholder="Город*"
                            v-model.trim="$v.city.$model" 
                            :class="{invalid: ($v.city.$dirty && $v.city.required)}" 
                        >
                        <small
                            class="form-helper__text invalid"
                            v-if="$v.city.$dirty && !$v.city.required"
                        >
                            Укажите город
                        </small>
                    </div>
                </div>
                <div class="form-input__group form-input__address-right">
                    <div class="form-input__block">
                        <label>Индекс</label>
                        <input 
                            class="form-input__person" 
                            type="text" 
                            name="index" 
                            placeholder="Индекс"
                            v-model.trim="$v.index.$model" 
                        >
                    </div>
                    <div class="form-input__block">
                        <label>Улица</label>
                        <input 
                            class="form-input__person" 
                            type="text" 
                            name="street" 
                            placeholder="Улица"
                            v-model.trim="$v.street.$model" 
                        >
                    </div>
                    <div class="form-input__block">
                        <label>Дом</label>
                        <input 
                            class="form-input__person" 
                            type="text" 
                            name="house" 
                            placeholder="Дом"
                            v-model.trim="$v.house.$model" 
                        >
                    </div>
                </div>
            </div>
            <div class="form-info__document">
                <h3 class="form-block__info-title">Паспорт:</h3>
                <div class="form-input__group">
                    <div class="form-input__block" :class="{ 'form-group__error': $v.typeDocument.$error }">
                        <label>Тип документа*</label>
                        <select 
                            class="form-input__person" 
                            name="typeDocument"
                            v-model.trim="$v.typeDocument.$model" 
                            :class="{invalid: ($v.typeDocument.$dirty && $v.typeDocument.required)}" 
                        >
                            <option value="pasport">Паспорт</option>
                            <option value="birth-certificate">Свидетельство о рождении</option>
                            <option value="driver's-license">Вод. удостоверение</option>
                        </select>
                        <small
                            class="form-helper__text invalid"
                            v-if="$v.typeDocument.$dirty && !$v.typeDocument.required"
                        >
                            Выберите тип документа
                        </small>
                    </div>
                    <div class="form-input__block">
                        <label>Серия</label>
                        <input 
                            class="form-input__person" 
                            type="text" 
                            name="name" 
                            placeholder="Серия"
                            v-model.trim="$v.series.$model" 
                        >
                    </div>
                    <div class="form-input__block">
                        <label>Номер</label>
                        <input 
                            class="form-input__person" 
                            type="text" name="name" 
                            placeholder="Номер"
                            v-model.trim="$v.numberDocument.$model" 
                        >
                    </div>
                </div>
                <div class="form-input__group">
                    <div class="form-input__block">
                        <label>Кем выдан</label>
                        <input 
                            class="form-input__person form-input__issued" 
                            type="text" 
                            name="issuedBy" 
                            placeholder="Кем выдан"
                            v-model.trim="$v.issuedBy.$model" 
                        >
                    </div>
                    <div class="form-input__block" :class="{ 'form-group__error': $v.dateIssue.$error }">
                        <label>Дата выдачи*</label>
                        <input 
                            class="form-input__person" 
                            type="text" 
                            name="dateIssue" 
                            placeholder="Дата выдачи*"
                            v-model.trim="$v.dateIssue.$model" 
                            :class="{invalid: ($v.dateIssue.$dirty && $v.dateIssue.required)}" 
                        >
                        <small
                            class="form-helper__text invalid"
                            v-if="$v.dateIssue.$dirty && !$v.dateIssue.required"
                        >
                            Укажите дату выдачи
                        </small>
                    </div>
                </div>
            </div>
            <div class="form-button__block">
                <button class="form-button" type="submit">Отправить</button>
            </div>
        </div>
    </form>
    <div :class="{'form-popup__positive' : showModalTrue}" class="form-positive" :click="disableM">
        <p class="form-positive__text">Форма успешно заполнена</p>
        <p class="form-positive__text">Данные отправлены.</p>
    </div>
    <div class="form-error" :class="{'form-popup__error': showModalFalse , 'form-popup__disabled' : !showModalFalse}" >
        <p class="form-error__text">Форма заполнена неправильно</p>
        <p class="form-error__text">Данные не отправлены.</p>
    </div>
  </div>
</template>


<script>
import Vue from 'vue'
import { required, minLength, numeric } from 'vuelidate/lib/validators'
import Multiselect from 'vue-multiselect'

Vue.component('multiselect', Multiselect)

export default {
    name: 'CryptoTable',
    components: { Multiselect },
    data: () => ({
        surname: '',
        name: '',
        birthday: '',
        phone: '',
        clients: [],
        city: '',
        typeDocument: '',
        dateIssue: '',
        showModalFalse: false,
        showModalTrue: false,
        options: [
            { name: 'VIP', code: 'vip' },
            { name: 'Проблемные', code: 'problems' },
            { name: 'ОМС', code: 'omc' }
        ]
    }),
    validations: {
        surname: {required, minLength: minLength(2)},
        name: {required, minLength: minLength(2)},
        middleName: {},
        birthday: {required},
        phone: {required, numeric, minLength: minLength(11)},
        gender: {},
        clients: {required},
        doctor:{},
        smsMail: {},
        index: {},
        country: {},
        region: {},
        street: {},
        house: {},
        city: {required},
        typeDocument: {required},
        series: {},
        numberDocument: {},
        issuedBy: {},
        dateIssue: {required},
    },
    methods: {
        submitHandler(e){
            if (this.$v.$invalid) {
                this.$v.$touch()
                this.showModalFalse = true
                if(this.showModalFalse) {
                    setTimeout(function(){
                        this.showModalFalse = false
                        console.log(this.showModalFalse)
                    }, 2000);
                }
            } else if (!this.$v.$invalid) {
                const formData = {
                    surname: this.surname ? this.surname : '',
                    name: this.name ? this.name : '',
                    middleName: this.middleName ? this.middleName : '',
                    birthday: this.birthday ? this.birthday : '',
                    phone: this.phone ? this.phone : '',
                    gender: this.gender ? this.gender : '',
                    clients: this.clients ? this.clients : '',
                    doctor: this.doctor ? this.doctor : '',
                    smsMail: this.doctor ? this.doctor : false,
                    index: this.index ? this.index : '',
                    country: this.country ? this.country : '',
                    region: this.region ? this.region : '',
                    city: this.city ? this.city : '',
                    street: this.street ? this.street : '',
                    house: this.house ? this.house : '',
                    typeDocument: this.typeDocument ? this.typeDocument : '',
                    series: this.series ? this.series : '',
                    numberDocument: this.numberDocument ? this.numberDocument : '',
                    issuedBy: this.issuedBy ? this.issuedBy : '',
                    dateIssue: this.dateIssue ? this.dateIssue : '',
                }
                this.showModalTrue = true
                this.showModalFalse = false
                if(this.showModalTrue) {
                    console.log('работает')
                }
            }
        },
        disableM: function () {
            this.showModalFalse = false
            console.log('работает')
        },
        addTag (newTag) {
            const tag = {
                name: newTag,
                code: newTag.substring(0, 2) + Math.floor((Math.random() * 10000000))
            }
            this.options.push(tag)
            this.value.push(tag)
        }
    }
}
</script>

<style src="vue-multiselect/dist/vue-multiselect.min.css"></style>

<style lang="sass">
.form 
    background-color: #EDEEF2
    padding: 50px
    width: 100%
    position: relative
    &-positive
        position: absolute
        top: 5%
        right: -500%
        padding: 10px 20px
        background-color: rgba(49,153,52, 0.7)
        transition: 0.3s
        &__text 
            color: white
    &-error
        position: absolute
        top: 5%
        right: -500%
        padding: 10px 20px
        background-color: rgba(258,8,0, 0.7)
        transition: 0.3s
        &__text 
            color: white
    &-popup
        &__positive 
            right: 5%
        &__error
            right: 5%
    &-title 
        color: grey
    &-block 
        display: flex
        background-color: white
        width: 100%
        height: 90%
        margin-top: 20px
        padding: 20px
        &__info 
            padding: 30px
            &-left 
                width: 40%
            &-right 
                width: 60%
        &__address
            display: flex
            justify-content: space-between
    &-date 
        width: 250px
    &-user
        &__logo 
            display: flex
            justify-content: center
            margin-bottom: 50px

    &-input
        &__address
            &-right
                justify-content: flex-end!important
        &__group 
            width: 100%
            display: flex
            align-items: center
            flex-wrap: wrap
            justify-content: space-between
            margin-top: 10px
        &__multiselect
            height: 22px!important
        &__person 
            width: 250px
        &__address 
            width: 500px
        &__block 
            display: flex
            flex-direction: column
            margin-top: 5px
            label 
                font-size: 15px
                color: #46A0E3
                font-weight: bold
            input
                margin-top: 5px
                height: 30px
                padding-left: 10px
                border: 1px solid grey
                border-radius: 3px
                outline: none
                font-size: 15px
            select
                margin-top: 5px
                height: 30px
                padding-left: 10px
                border: 1px solid grey
                border-radius: 3px
                outline: none
                font-size: 15px
            &-checkbox  
                display: flex
                align-items: center
                label
                    margin-right: 10px
                    font-size: 12px
                input
                    width: 15px
                    height: 15px
            &-multiselect
                width: 100%
        &__issued 
            width: 450px
    &-block
        &__info
            &-title 
                margin-top: 50px
    &-button
        color: white
        background-color: #46A0E3
        border: none
        border-radius: 3px
        padding: 10px 20px
        cursor: pointer
        outline: none
        &:hover 
            background-color: #0081E3
        &:active 
            background-color: black
        &__block
            margin-top: 50px
            display: flex
            justify-content: flex-end

    &-helper
        &__text
            font-size: 10px
            color: red
        &__error
            input
                border: 1px solid red
            select
                border: 1px solid red

.multiselect
    &__tags
        padding: 4px
    &__tags input 
        height: 22px


@media (max-width: 1600px)
    .form 
        &-block 
            height: 100%
            &__info
                &-left
                    width: 30%
                &-left .form-input__block
                    width: 100%
                &-left .form-input__block input
                    width: 100%
                &-left .form-input__block select
                    width: 100%

                &-right 
                    width: 70%
        &-group
            &__inputs
                &-last
                    display: flex
                    align-items: flex-start
                    flex-direction: column
        &-input
            &__block
                &-checkbox
                    margin-top: 10px
@media (max-width: 1380px)
    .form 
        &-input
            &__address
                width: 400px
            &__issued
                width: 400px
            &__address 
                &-right 
                    justify-content: flex-start!important
        &-block 
            &__address 
                flex-direction: column
            &__info
                &-right 
                    padding-left: 150px
                &-right input 
                    width: 400px
                &-right select 
                    width: 400px
@media (max-width: 1380px)
    .form
        &-block
            overflow: auto
            &__info
                &-left
                    width: 50%
                &-right 
                    width: 50%
                    padding-left: 0px
                &-right .form-input__block
                    width: 100%
                &-right input 
                    width: 100%
                &-right select 
                    width: 100%
                &-title 
                    margin-top: 10px
        &-button 
            &__block 
                margin-top: 30px

@media (max-width: 768px)
    .form
        &-block
            flex-direction: column
            &__info
                padding: 0px
                &-left
                    width: auto
                &-right 
                    width: auto

@media (max-width: 500px)
    .form 
        padding: 20px
        &-block 
            height: 90%
        &-error
            &__text
                font-size: 12px
    
@media (max-width: 380px)
    .form 
        padding: 10px
        &-title 
            font-size: 20px


</style>
