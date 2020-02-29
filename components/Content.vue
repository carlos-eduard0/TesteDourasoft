<template>
<view class="content">
  <view class="itens-busca">
    <view class="inputBusca">
      <text-input
        class="input"
        v-model="place"
        placeholder="Informe o nome da cidade"
        placeholderTextColor="#A9A9A9"
      />
    </view>
    <TouchableOpacity class="btn" :on-press="getWeatherData" required>
      <MaterialIcons class="icon" name="search" />
    </TouchableOpacity>
  </view>
      <view class="tempPrincipal">
        <text class="textCity">{{city}}</text>
      <text class="text">{{temperatura}}</text>
    </view>

    <view class="card">
        <view class="info">
        <MaterialIcons class="icon-card" name="location-city" />
        <text class="text-card">{{weather_descrip}}</text>
      </view>
      <view class="info">
        <MaterialIcons class="icon-card" name="wb-sunny" />
        <text class="text-card">{{temp_max}}</text>
      </view>
      <view class="info">
        <MaterialIcons class="icon-card" name="ac-unit" />
         <text class="text-card">{{temp_min}}</text>
      </view>
       <view class="info">
        <MaterialIcons class="icon-card" name="opacity" />
         <text class="text-card">{{humidity}}</text>
      </view>
      
    </view>
</view>

</template>

<style>
.content {
  justify-content: center;
  align-items: center;
  flex-direction: column;
}
.tempPrincipal {
  position: absolute;
  z-index: 5;
  top: 50%;
  margin-top: 32px;
}
.text {
  text-align: center;
  color: #fff;
  font-size: 45px;
}
.text-card{
  text-align: center;
   color: rgb(117, 131, 146);
  font-size: 30px;
}
.textCity{
  color: #fff;
   text-align: center;
  font-size: 46px;
}
.itens-busca {
  position: absolute;
  top: 70px;
  left: 20px;
  right: 20px;
  z-index: 5;
  flex-direction: row;
}

.inputBusca {
  flex: 1;
  height: 50px;
  background-color: #fff;
  color: #333;
  border-radius: 25px;
  font-size: 16px;
}

.input {
  padding-top: 15px;
  padding-bottom: 15px;
  padding-left: 15px;
  color: rgb(104, 104, 104);
}
.icon {
  color: rgb(77, 90, 100);
  font-size: 30px;
}
.btn {
  width: 50px;
  height: 50px;
  background-color: rgb(189, 209, 235);
  border-radius: 25px;
  justify-content: center;
  align-items: center;
  margin-left: 15px;
}
.card {
  position: relative;
  top: 133%;
  width: 100%;
  min-height: 352px;
  background-color: rgb(255, 255, 255);

}
.icon-card{
  font-size: 40px;
  color: rgb(117, 131, 146);
}
.info{
  margin-top: 10.2%;
  margin-left: 6%;
  margin-right: 7%;
  flex-direction: row;
  align-items: center;
  justify-content: space-between;
}
</style>

<script>
import axios from "axios";
import { TouchableOpacity } from "react-native";
import { MaterialIcons } from "@expo/vector-icons";
export default {
  data() {
    return {
      weather_descrip: "",
      city: "",
      temperatura: "",
      temp_unit: "°C",
      place: "",
      temp_min: '',
      temp_max: '',
      humidity: '',
      temp_umid:"%",
      status:"",
    };
  },
  components: {
    MaterialIcons,
    TouchableOpacity
  },
  methods: {
    getWeatherData: async function() {
      if(!this.place){
        alert("Informe a cidade para continuar");
      }

      else{
      encoded_place = this.place;
      zip=this.place;
      api_key = "f0a2c2834ce0564476a07dc2627a5baf";
      await axios
        .get("https://api.openweathermap.org/data/2.5/weather?q=" +encoded_place  +"&units=metric" +"&appid=" +api_key + "&lang=pt_br")
        .catch(function(error){
          if(error.response){
            alert("Cidade não encontrada, por favor tente");
          }
        })
        .then(response => {
          this.weather_descrip = response["data"]["weather"][0]["description"];
          this.temperatura = parseInt(response["data"]["main"]["temp"]) + this.temp_unit;
          this.city = response["data"]["name"];
          this.temp_min = parseInt(response['data']['main']['temp_min']) + this.temp_unit;
          this.temp_max = parseInt(response['data']['main']['temp_max']) + this.temp_unit;
          this.humidity = parseInt(response['data']['main']['humidity']) + this.temp_umid;
          this.place="";
        });
      }
    }
  }
};
</script>