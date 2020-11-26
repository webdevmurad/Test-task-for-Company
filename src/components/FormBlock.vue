<template>
  <div class="body-block">
    <h2 class="body-block__title">Форма заполнения данных</h2>
    <form class="body-form" @submit.prevent="submitHandler">
        <div class="form-person__inputs">
            <h3 class="form-title">Контактная информация:</h3>
            <div class="form-person__input-blocks form-display__blocks">
                <div class="form-person__input-block form-display__block" :class="{ 'form-input__error': $v.surname.$error }">
                    <label>Фамилия*</label>
                    <input 
                        id="surname"
                        class="" 
                        type="text" 
                        name="surname" 
                        placeholder="Фамилия*"
                        v-model.trim="$v.surname.$model" 
                        :class="{invalid: ($v.surname.$dirty && !$v.surname.required)}" 
                    >
                    <small
                        class=" invalid"
                        v-if="$v.surname.$dirty && !$v.surname.required"
                    >Поле Фамилия не должно быть пустым</small>
                    <small
                        class=" invalid"
                        v-if="$v.surname.$dirty && !$v.surname.minLength"
                    >
                        Введите две или более буквы
                    </small>
                </div>
                <div class="form-person__input-block form-display__block" :class="{ 'form-input__error': $v.name.$error }">
                    <label for="name">Имя*</label>
                    <input 
                        v-model.trim="$v.name.$model" 
                        :class="{invalid: ($v.name.$dirty && $v.name.required)}" 
                        class="" 
                        type="text" 
                        name="name" 
                        placeholder="Имя*"
                    >
                    <small
                        class=" invalid"
                        v-if="$v.name.$dirty && !$v.name.required"
                    >Поле Фамилия не должно быть пустым</small>
                    <small
                        class=" invalid"
                        v-if="$v.name.$dirty && !$v.name.minLength"
                    >
                        Введите две или более буквы
                    </small>
                </div>
                <div class="form-person__input-block form-display__block">
                    <label for="middleName">Отчество</label>
                    <input 
                        class="" 
                        type="text" 
                        name="middleName" 
                        v-model.trim="$v.middleName.$model" 
                        placeholder="Отчество"
                    >
                </div>
                <div class="form-person__input-block form-display__block" :class="{ 'form-input__error': $v.birthday.$error }">
                    <label>Дата рождения*</label>
                    <input 
                        v-model.trim="$v.birthday.$model" 
                        :class="{invalid: ($v.birthday.$dirty && $v.birthday.required)}" 
                        class=""  
                        type="date" 
                        placeholder="Дата рождения*"
                    >
                    <small
                        class=" invalid"
                        v-if="$v.name.$dirty && !$v.name.required"
                    >
                        Укажите дату рождения
                    </small>
                </div>
                <div class="form-person__input-block form-display__block" :class="{ 'form-input__error': $v.phone.$error }">
                    <label>Номер телефона*</label>
                    <input 
                        type="tel" 
                        name="phone" 
                        id="phone"
                        autocomplete="tel"
                        maxlength="14"
                        v-phone
                        placeholder="Номер телефона*"
                        v-model.trim="$v.phone.$model" 
                        :class="{invalid: ($v.phone.$dirty && $v.phone.required)}" 
                    />
                    <small
                        class=" invalid"
                        v-if="$v.phone.$dirty && !$v.phone.required"
                    >
                        Укажите номер телефона
                    </small>
                </div>
                <div class="form-person__select-block form-display__block">
                    <label>Пол</label>
                    <select 
                        class="" 
                        name="gender"
                        v-model.trim="$v.gender.$model" 
                    >
                        <option value="male">Мужской</option>
                        <option value="male">Женский</option>
                    </select>
                </div>
                <div class="form-person__multiselect-block form-display__block" :class="{ 'form-input__error': $v.clients.$error }">
                    <label>Группа клиентов*</label>
                    <multiselect 
                        class=""
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
                        class=" invalid"
                        v-if="$v.clients.$dirty && !$v.clients.required"
                    >
                        Выберите одно или несколько
                    </small>
                </div>
                <div class="form-person__select-block form-display__block">
                    <label>Лечащий врач</label>
                    <select 
                        class="" 
                        name="doctor"
                        v-model.trim="$v.doctor.$model" 
                    >
                        <option value="ivanov">Иванов</option>
                        <option value="zakharov">Захаров</option>
                        <option value="chernysheva">Чернышева</option>
                    </select>
                </div>
            </div>
        </div>
        <div class="form-address__inputs">
            <h3 class="form-title">Адрес:</h3>
            <div class="form-address__input-blocks form-display__blocks"> 
                <div class="form-address__input-block form-display__block">
                    <label>Страна</label>
                    <input 
                        type="text" 
                        name="country" 
                        placeholder="Страна"
                        v-model.trim="$v.country.$model" 
                    >
                </div>
                <div class="form-address__input-block form-display__block">
                    <label>Область</label>
                    <input 
                        type="text" 
                        name="region" 
                        placeholder="Область"
                        v-model.trim="$v.region.$model" 
                    >
                </div>
                <div class="form-address__input-block form-display__block" :class="{ 'form-input__error': $v.city.$error }">
                    <label>Город*</label>
                    <input 
                        type="text" 
                        name="city" 
                        placeholder="Город*"
                        v-model.trim="$v.city.$model" 
                        :class="{invalid: ($v.city.$dirty && $v.city.required)}" 
                    >
                    <small
                        class=" invalid"
                        v-if="$v.city.$dirty && !$v.city.required"
                    >
                        Укажите город
                    </small>
                </div>
                <div class="form-address__input-block form-display__block">
                    <label>Индекс</label>
                    <input 
                        class="" 
                        type="text" 
                        name="index" 
                        placeholder="Индекс"
                        v-model.trim="$v.index.$model" 
                    >
                </div>
                <div class="form-address__input-block form-display__block">
                    <label>Улица</label>
                    <input 
                        class="" 
                        type="text" 
                        name="street" 
                        placeholder="Улица"
                        v-model.trim="$v.street.$model" 
                    >
                </div>
                <div class="form-address__input-block form-display__block">
                    <label>Дом</label>
                    <input 
                        class="" 
                        type="text" 
                        name="house" 
                        placeholder="Дом"
                        v-model.trim="$v.house.$model" 
                    >
                </div>
            </div>
        </div>
        <div class="form-pasport__inputs">
            <h3 class="form-title">Паспорт:</h3>
            <div class="form-pasport__input-blocks form-display__blocks">
                <div class="form-pasport__select-block form-display__block" :class="{ 'form-input__error': $v.typeDocument.$error }">
                    <label>Тип документа*</label>
                    <select 
                        class="" 
                        name="typeDocument"
                        v-model.trim="$v.typeDocument.$model" 
                        :class="{invalid: ($v.typeDocument.$dirty && $v.typeDocument.required)}" 
                    >
                        <option value="pasport">Паспорт</option>
                        <option value="birth-certificate">Свидетельство о рождении</option>
                        <option value="driver's-license">Вод. удостоверение</option>
                    </select>
                    <small
                        class=" invalid"
                        v-if="$v.typeDocument.$dirty && !$v.typeDocument.required"
                    >
                        Выберите тип документа
                    </small>
                </div>
                <div class="form-pasport__input-block form-display__block">
                    <label>Серия</label>
                    <input 
                        class="" 
                        type="text" 
                        name="name" 
                        placeholder="Серия"
                        v-model.trim="$v.series.$model" 
                    >
                </div>
                <div class="form-pasport__input-block form-display__block">
                    <label>Номер</label>
                    <input 
                        class="" 
                        type="text" name="name" 
                        placeholder="Номер"
                        v-model.trim="$v.numberDocument.$model" 
                    >
                </div>
                <div class="form-pasport__input-block form-display__block">
                    <label>Кем выдан</label>
                    <input 
                        class="" 
                        type="text" 
                        name="issuedBy" 
                        placeholder="Кем выдан"
                        v-model.trim="$v.issuedBy.$model" 
                    >
                </div>
                <div class="form-pasport__input-block form-display__block" :class="{ 'form-input__error': $v.dateIssue.$error }">
                    <label>Дата выдачи*</label>
                    <input 
                        class="" 
                        type="text" 
                        name="dateIssue" 
                        placeholder="Дата выдачи*"
                        v-model.trim="$v.dateIssue.$model" 
                        :class="{invalid: ($v.dateIssue.$dirty && $v.dateIssue.required)}" 
                    >
                    <small
                        class=" invalid"
                        v-if="$v.dateIssue.$dirty && !$v.dateIssue.required"
                    >
                        Укажите дату выдачи
                    </small>
                </div>
            </div>
        </div>
        <div class="form-submit">
            <div class="form-checkbox">
                <label for="sms">Не отправлять СМС</label>
                <input 
                    type="checkbox" 
                    name="sms" 
                    id="sms"
                    v-model.trim="$v.smsMail.$model" 
                >
            </div>
            <button class="form-submit__button" type="submit">Отправить</button>
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

<script src="https://cdnjs.cloudflare.com/ajax/libs/vue/2.5.3/vue.min.js"></script>

<script>
import Vue from 'vue'
import { required, minLength, numeric } from 'vuelidate/lib/validators'
import Multiselect from 'vue-multiselect'

Vue.directive('phone', {
    bind(el) {  
        el.oninput = function(e) {
        if (!e.isTrusted) {
            return;
        }

        const x = this.value.replace(/\D/g, '').match(/(\d{0,3})(\d{0,3})(\d{0,4})/);
        this.value = !x[2] ? x[1] :  '(' + x[1] + ') ' + x[2] + (x[3] ? '-' + x[3] : '');
        el.dispatchEvent(new Event('input'));
        }
    },
});

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
        phone: {required},
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
                console.log(formData)
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


.body
    &-block
        margin: auto
        position: relative
        &__title 
            padding: 10px 0
            color: #0078D4
    &-form
        width: 1200px


.form
    &-title
        color: #0078D4
        margin: 10px 0
    &-display 
        &__blocks 
            display: flex
            flex-wrap: wrap 
            justify-content: space-between
        &__block 
            display: flex
            flex-direction: column
            margin-top: 10px
            small 
                margin-top: 3px
                padding-left: 5px
                color: red
            input 
                font-size: 15px
                width: 350px
                height: 40px
                border-radius: 5px
                border: 1px solid #E8E8E8
                padding-left: 10px
                outline: none
                &:hover 
                    border: 1px solid #0063AF
            select 
                font-size: 15px
                width: 350px
                height: 40px
                border-radius: 5px
                border: 1px solid #E8E8E8
                padding-left: 10px
                outline: none
                &:hover 
                    border: 1px solid #0063AF
            label 
                padding-left: 10px
                margin-bottom: 5px
    &-submit 
        display: flex
        flex-direction: row
        justify-content: center
        &__button 
            padding: 10px 20px
            border-radius: 5px
            border: none
            color: white 
            background-color: #0078D4
            outline: none
            &:hover 
                cursor: pointer
                background-color: #0063AF
            &:active 
                background-color: black
    &-checkbox 
        margin-right: 30px
        display: flex
        align-items: center
        label
            font-size: 12px
            padding-right: 10px

    &-input
        &__error
            input 
                border: 1px solid red
                
            select
                border: 1px solid red
            .multiselect__tags
                border: 1px solid red

    &-positive 
        position: absolute
        top: 5%
        right: -500%
        padding: 15px 30px
        color: white 
        background-color: rgba(87,246,59, 0.6)
        transition: 0.3s
    &-error 
        position: absolute
        top: 5%
        right: -500%
        padding: 15px 30px
        color: white 
        background-color: rgba(255,0,0, 0.6)
        transition: 0.3s
    &-popup
        &__positive
            right: 5%
        &__error
            right: 5%
    

.multiselect
    width: 350px
    &__tags
        input 
            outline: none
            height: 22px
            border-radius: 5px
            border: 1px solid #E8E8E8
            &:hover 
                border: 1px solid #0063AF

@media (max-width: 1250px)
    .body
        &-form
            width: 720px

@media (max-width: 768px)
    .body
        &-form
            width: 350px
    .form 
        &-submit 
            padding: 20px 0
        &-positive
            top: 1% 
            p 
                font-size: 12px
        &-error 
            top: 1%
            p 
                font-size: 12px

@media (max-width: 400px)
    .body
        &-form
            width: 300px
            margin: auto
        &-block
            &__title
                padding: 0px 10px 
                text-align: center
    .form
        &-title 
            padding-left: 10px
        &-display
            &__block
                input 
                    width: 250px
                select 
                    width: 250px

            &__blocks 
                justify-content: center

        &-person 
            &__multiselect
                &-block 
                    .multiselect
                        width: 290px

</style>
