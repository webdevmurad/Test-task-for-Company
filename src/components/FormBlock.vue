<template>
  <div class="form">
    <h2 class="form-title">Форма заполнения данных</h2>
    <form class="form-block" @submit.prevent="submitHandler">
        <div class="form-block__info form-block__info-left">
            <div class="form-user__logo">
                <img src="../assets/user.png" alt="user">
            </div>
            <div class="form-input__group">
                <div class="form-input__block" :class="{ 'form-group--error': $v.surname.$error }">
                    <label>Фамилия*</label>
                    <input 
                        id="surname"
                        class="form-input__person" 
                        type="text"  
                        placeholder="Фамилия*"
                        v-model.trim="$v.surname.$model" 
                        :class="{invalid: ($v.surname.$dirty && !$v.surname.required)}" 
                    >
                </div>
                <div class="form-input__block">
                    <label for="name">Имя*</label>
                    <input 
                        v-model.trim="name" 
                        :class="{invalid: ($v.name.$dirty && $v.name.required)}" 
                        class="form-input__person" 
                        type="text" 
                        name="name" 
                        placeholder="Имя*"
                    >
                </div>
                <div class="form-input__block">
                    <label for="middleName">Отчество</label>
                    <input class="form-input__person" type="text" name="middleName" placeholder="Отчество">
                </div>
            </div>
            <div class="form-input__group">
                <div class="form-input__block">
                    <label>Дата рождения*</label>
                    <input class="form-input__person"  type="date" placeholder="Дата рождения*">
                </div>
                <div class="form-input__block">
                    <label>Номер телефона*</label>
                    <input class="form-input__person" type="text" name="name" placeholder="Номер телефона*">
                </div>
            </div>
            <div class="form-input__group">
                <div class="form-input__block">
                    <label for="gender">Пол</label>
                    <select class="form-input__person" name="gender">
                        <option value="male">Мужской</option>
                        <option value="male">Женский</option>
                    </select>
                </div>
                <div class="form-input__block">
                    <label for="doctor">Лечащий врач</label>
                    <select class="form-input__person" name="doctor">
                        <option value="ivanov">Иванов</option>
                        <option value="zakharov">Захаров</option>
                        <option value="chernysheva">Чернышева</option>
                    </select>
                </div>
            </div>
            <div class="form-input__group">
                <div class="form-input__block">
                    <label for="doctor">Группа клиентов*</label>
                    <select multiple class="form-multiselect" name="client">
                        <option value="vip">VIP</option>
                        <option value="problem">Проблемные</option>
                        <option value="oms">ОМС</option>
                    </select>
                </div>
                <div class="form-input__block-checkbox">
                    <label for="sms">Не отправлять СМС</label>
                    <input type="checkbox" name="sms" id="sms">
                </div>
            </div>
        </div>
        <div class="form-block__info form-block__info-right">
            <div class="form-block__address">
                <h3 class="form-block__info-title">Адрес:</h3>
                <div class="form-input__group">
                    <div class="form-input__block">
                        <label>Страна</label>
                        <input class="form-input__person form-input__address" type="text" name="name" placeholder="Страна">
                    </div>
                    <div class="form-input__block">
                        <label>Область</label>
                        <input class="form-input__person form-input__address" type="text" name="name" placeholder="Область">
                    </div>
                    <div class="form-input__block">
                        <label>Город*</label>
                        <input class="form-input__person form-input__address" type="text" name="name" placeholder="Город*">
                    </div>
                </div>
                <div class="form-input__group">
                    <div class="form-input__block">
                        <label>Индекс</label>
                        <input class="form-input__person" type="text" name="name" placeholder="Индекс">
                    </div>
                    <div class="form-input__block">
                        <label>Улица</label>
                        <input class="form-input__person" type="text" name="name" placeholder="Улица">
                    </div>
                    <div class="form-input__block">
                        <label>Дом</label>
                        <input class="form-input__person" type="text" name="name" placeholder="Дом">
                    </div>
                </div>
            </div>
            <div class="form-info__document">
                <h3 class="form-block__info-title">Паспорт:</h3>
                <div class="form-input__group">
                    <div class="form-input__block">
                        <label for="doctor">Тип документа*</label>
                        <select class="form-input__person" name="doctor">
                            <option value="vip">Паспорт</option>
                            <option value="problem">Свидетельство о рождении</option>
                            <option value="oms">Вод. удостоверение</option>
                        </select>
                    </div>
                    <div class="form-input__block">
                        <label>Серия</label>
                        <input class="form-input__person" type="text" name="name" placeholder="Серия">
                    </div>
                    <div class="form-input__block">
                        <label>Номер</label>
                        <input class="form-input__person" type="text" name="name" placeholder="Номер">
                    </div>
                </div>
                <div class="form-input__group">
                    <div class="form-input__block">
                        <label>Кем выдан</label>
                        <input class="form-input__person form-input__issued" type="text" name="name" placeholder="Кем выдан">
                    </div>
                    <div class="form-input__block">
                        <label>Дата выдачи*</label>
                        <input class="form-input__person" type="text" name="name" placeholder="Дата выдачи*">
                    </div>
                </div>
            </div>
            <div class="form-button__block">
                <button class="form-button" type="submit">Отправить</button>
            </div>
        </div>
    </form>
  </div>
</template>


<script>

import { required, minLength } from 'vuelidate/lib/validators'


export default {
    name: 'CryptoTable',
    data: () => ({
        surname: '',
        name: '',
        middleName: '',
        birthday: '',
        phone: '',
        gender: '',
        clients: '',
        doctor: '',
        smsMail: false,
        index: '',
        country: '',
        region: '',
        city: '',
        street: '',
        house: '',
        typeDocument: '',
        series: '',
        numberDocument: '',
        issuedBy: '',
        dateIssue: '',

    }),
    validations: {
        surname: {required, minLength: minLength(2)},
        name: {required, minLength: minLength(2)}
    },
    methods: {
        submitHandler(){
            if (this.$v.$invalid) {
                this.$v.$touch()
                console.log(this.validations)
                return 
            }
        }
    }
}
</script>

<style lang="sass">
.form 
    background-color: #EDEEF2
    padding: 50px
    width: 100%
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
    &-date 
        width: 250px
    &-user
        &__logo 
            display: flex
            justify-content: center
            margin-bottom: 50px

    &-input
        &__group 
            display: flex
            align-items: center
            flex-wrap: wrap
            justify-content: space-between
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


</style>
