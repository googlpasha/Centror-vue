<template>
  <div class="training">
    <div class="container">
      <div class="row">
        <div class="col col-12">
          <h1 class="program__name">{{training.Program_Name}}</h1>
          <h3>Никогда не поздно научиться. Сделай это сегодня.</h3>
        </div>
      </div>
      <div class="row">
        <div class="description col col-12 col-md-6">
          <p>{{training.Program_Full_Description}}</p>
        </div>
        <div class="description col col-12 col-md-6">
          <h4 class="text-center">Преподавательский состав</h4>
          <div v-for="(trainingTeacher, index) in training.lectors"
          :key="index" class="row teachers">
            <div class="teacher col col-12">
              <div class="avatar">
                <img
                    class="avatar"
                    :src="host + trainingTeacher.Photo.url"
                >
              </div>
              <h4>{{trainingTeacher.First_Name}} {{trainingTeacher.Last_Name}}</h4>
            </div>
          </div>
          <div class="row">
            <div class="order col col-12">
              <h5>Стоимость программы</h5>
              <h5>140 000р.</h5>
              <button type="button" data-toggle="modal" data-target="#exampleModal" class="btn btn-light">
                Записаться на обучение
              </button>
            </div>
          </div>
        </div>
      </div>
      <!-- facebook -->
      <div class="row">
        <div class="col-lg-12">
          <h3 class="facebook__title">Отзывы из <span class="facebook__title__blue">Facebook</span></h3>
        </div>
      </div>
      <div class="row">
        <div class="col-lg-12">
          <div class="facebook__container">
            <div class="fb-comments" :data-href="training.Facebook_Link" data-width="500px" data-numposts="5"></div>
          </div>
        </div>
      </div>
    </div>
    <div class="modal fade bd-example-modal-lg" id="exampleModal" tabindex="-1" role="dialog" aria-labelledby="exampleModalLabel" aria-hidden="true">
      <div class="modal-dialog" role="document">
        <div class="modal-content modalWindow">
          <div class="modal-header">
            <h5 class="modal-title" id="exampleModalLabel">Контактная информация</h5>
          </div>
            <div class="modal-body" style="padding-bottom:0">
              <div class="input-group">
                <p class="inputBlock">
                  <label for="SecondName">Фамилия:</label>
                  <input v-model="second_name" id="SecondName" type="text" class="form-control" style="margin-right:20px">
                </p>
                <p class="inputBlock inputBlockLeft">
                  <label for="email">Адрес электронной почты:</label>
                  <input v-model="email_adress" id="email" type="text" class="form-control">
                </p>
            </div>
              <div class="input-group">
                <p class="inputBlock">
                  <label for="name">Имя:</label>
                  <input v-model="first_name" id="name" type="text" class="form-control" style="margin-right:20px">
                </p>
                <p class="inputBlock inputBlockLeft">
                  <label for="number">Контактный телефон:</label>
                  <input v-model="phone_number" id="number" type="text" class="form-control">
                </p>
                <p class="inputBlock">
                  <label for="date">Дата рождения:</label>
                  <datepicker v-model="date_picked" id="date" :language="ru" class="date"></datepicker>
                </p>
                <p class="inputBlock inputBlockLeft">
                  <label for="cityid" class="cityLabel">Город:</label>
                  <input v-model="city" id="cityid" type="text" class="form-control">
                </p>
            </div>
          </div>
          <div class="modal-footer" style="padding-top:0">
            <button v-on:click="sub" type="button" class="submitButton">Перейти к оплате</button>
          </div>
          <div v-for="(err,index) in errors" :key="index">
              {{err}}
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import Datepicker from 'vuejs-datepicker';
import {ru} from 'vuejs-datepicker/dist/locale'
import { v4 as uuidv4 } from 'uuid';
export default {
  name: 'training',
  components: {
    Datepicker
  },
  data () {
    return {
      second_name: '',
      email_adress: '',
      first_name: '',
      phone_number: '',
      date_picked: '',
      city: '',
      errors: [],
      ru: ru,
      url: {
          ProgramApiLink: this.$store.getters.takeProgramm,
          SubcategoriesApilink: this.$store.getters
      },
      // state: {
      //   date: new Date(2016, 9,  16)
      // },
      training: {},
      host: this.$store.getters.takeHost,
    }
  },
  async created () {
    const respones = await fetch(this.url.ProgramApiLink + '/' + this.$route.params.id)
    const data = await respones.json()

    this.training = data
  },
  mounted () {
  },
  methods: {
    sub: function(event){


      // var data = JSON.stringify({
      //   "amount": {
      //     "value": "2.00",
      //     "currency": "RUB"
      //   },
      //   "payment_method_data": {
      //     "type": "bank_card"
      //   },
      //   "confirmation": {
      //     "type": "redirect",
      //     "return_url": "https://www.merchant-website.com/return_url"
      //   },
      //   "description": "Заказ №72"
      // });

      // var xhr = new XMLHttpRequest();
      // xhr.withCredentials = true;

      // xhr.addEventListener("readystatechange", function () {
      //   if (this.readyState === 4) {
      //     console.log(this.responseText);
      //   }
      // });

      // xhr.open("POST", "https://payment.yandex.net/api/v3/payments");
      // xhr.setRequestHeader("content-type", "application/json");
      // xhr.setRequestHeader("authorization", "Basic Njc2NDUwOnRlc3RfT2hjWFJ3RFNjZEJrbTdmSWlyRXRxUm5iU2xMY0hURVp6WjJraGNOVjVlSQ==");
      // xhr.setRequestHeader("idempotence-key", "02347fc4-a1f0-49db-807e-f0d67c2ed5a5");
      // xhr.setRequestHeader("cache-control", "no-cache");
      // xhr.setRequestHeader("postman-token", "ab7512de-557e-e07a-3eeb-3b88451854fb");

      // xhr.send(data);


        // fetch("https://payment.yandex.net/api/v3/payments", {
        //   body: {
        //       amount: {
        //         value: "2.00",
        //         currency: "RUB"
        //       },
        //       payment_method_data: {
        //         type:"bank_card"
        //       },
        //       confirmation: {
        //         type: "redirect",
        //         return_url: "https://www.merchant-website.com/return_url"
        //       },
        //       description: "Заказ №72"      
        //       },
        //       headers: {
        //         Authorization: "Basic Njc2NDUwOnRlc3RfT2hjWFJ3RFNjZEJrbTdmSWlyRXRxUm5iU2xMY0hURVp6WjJraGNOVjVlSQ==",
        //         "Content-Type": "application/json",
        //         "Idempotence-Key": uuidv4()
        //       },
        //       method: "POST"
        // })

        
          axios.post('https://payment.yandex.net/api/v3/payments/',{
              
              "headers": {
                "async": true,
                'Access-Control-Allow-Origin': '*',
                "content-type": "application/json",
                "authorization": "Basic Njc2NDUwOnRlc3RfT2hjWFJ3RFNjZEJrbTdmSWlyRXRxUm5iU2xMY0hURVp6WjJraGNOVjVlSQ==",
                "idempotence-key": uuidv4(),
              },
              "data": {
                "amount": {
                  "value": "",
                  "currency": "RUB"
                },
                  "confirmation": {
                  "type": "embedded"
                },
                  "capture": true,
                  "description": "Заказ №72"
              }

              // "last_name": this.second_name,
              // "first_name": this.first_name,
              // "city": this.city,
              // "email": this.email_adress,
              // "phone": this.phone_number,
              // "program": this.$route.params.id
              
          })
          .then(response => { 
              console.log(response);
              // this.second_name = '',
              // this.first_name = '',
              // this.city = '',
              // this.email_adress = '',
              // this.phone_number = '',
              // this.$route.params.id = ''
              // this.$router.push('/auth');

              //window.location.href = "/auth/"+ this.$route.params.id;
          })
          .catch(error => {
              console.log(error.response);
              //this.errors.push('Не верный логин или пароль'); 
          });


    }
  }
}
</script>

<style>

.vdp-datepicker *{
  background: #595C61;
  color: #fff;
  border:#595C61;
  height: 25px;
}
.vdp-datepicker__calendar{
  background-color: #495A67;
}
</style>

<style lang="scss" scoped>
.program__name{
  margin-top: 30px;
}
.training {
  display: flex;
  flex-direction: column;
  flex: 1 1 auto;
  color: whitesmoke;

  .container {
    display: flex;
    flex-direction: column;
    flex: 1 1 auto;

    .row:nth-child(2) {
      flex: 1 1 auto;

      .description:nth-child(1) {
        padding: 1rem 1.5rem;
        border-radius: 15px;
        background-color: #435A6E;
      }

      .description:nth-child(2) {
        padding: 1rem 1.5rem;

        .teachers .teacher{
          display: flex;
          align-items: center;
          margin: 1rem 0;

          h4 {
            margin: 0;
          }

          .avatar {
            width: 50px;
            height: 50px;
            background-color: grey;
            margin-right: 1rem;
          }
        }

        .order {
          display: flex;
          flex-direction: column;
          align-items: flex-end;
          margin-top: 3rem;
        }
      }
    }
  }
}
.modalWindow{
  background: linear-gradient(0deg, rgba(97, 139, 170, 0.44), rgba(97, 139, 170, 0.44)), #3D4A5B;
  font-family: Montserrat;
  width: 520px;
}
.modal-header, .modal-body, .modal-footer{
  border: none;
}
.inputBlock{
  width: 220px;
}
.inputBlockLeft{
  margin-left: 25px;
}
label{
  font-size: 15px;
}
.modal-header{
  font-size: 18px;
  padding: 10px;
}
.modal-body{
  padding-top: 0;
}
.form-control{
  background: #595C61;
  color: #fff;
  border:#595C61;
  height: 25px;
  width: 230px;
}
.submitButton{
  background: #495A67;
  border-radius: 5px;
  color: #fff;
  border: #495A67;
}
.facebook__title{
  margin-top: 30px;
}
.facebook__title__blue{
  color: #3b5998;
}
.facebook__container{
  background: #fff;
}
.cityLabel{
  margin-bottom: 2px;
}
label{
  margin-left: 5px;
}
#date{
  width: 230px;

}
.date{
  width: 225px;
  margin-left: 10px;
}
#cityid{
  width: 230px;
}

</style>
