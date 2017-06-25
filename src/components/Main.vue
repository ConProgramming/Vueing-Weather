<template>
<div class="container">
	<div class="row">
	    <div class="input-group">
          <span class="input-group-addon" id="basic-addon1">Zipcode</span>
          <input type="text" maxlength="5" onkeypress="return (event.charCode == 8 || event.charCode == 0 || event.charCode == 13) ? null : event.charCode >= 48 && event.charCode <= 57" class="form-control" placeholder="78015" aria-describedby="basic-addon1" v-model="zipcode" v-on:keyup.enter="pulljson(zipcode,country)">
          
          <!-- <span class="input-group-addon" id="basic-addon1">Country</span>
          <input type="text" class="form-control" placeholder="United States" aria-describedby="basic-addon1" v-model="country"> -->
          
          <span class="input-group-btn" id="basic-addon1">
          <button class="btn" type="button" v-on:click="pulljson(zipcode,country)"><span class="glyphicon glyphicon-refresh"></span></button></span>
      
        </div>
	    
		<!-- <div class="col">
			<div class="weather-card one">
				<div class="top">
					<div class="wrapper">
						<div class="mynav">
							<a href="javascript:;"><span class="lnr lnr-chevron-left"></span></a>
							<a href="javascript:;"><span class="lnr lnr-cog"></span></a>
						</div>
						<h1 class="heading">Clear night</h1>
						<h3 class="location">{{location}}</h3>
						<p class="temp">
							<span class="temp-value">20</span>
							<span class="deg">0</span>
							<a href="javascript:;"><span class="temp-type">C</span></a>
						</p>
					</div>
				</div>
				<div class="bottom">
					<div class="wrapper">
						<ul class="forecast">
							<a href="javascript:;"><span class="lnr lnr-chevron-up go-up"></span></a>
							<li class="active">
								<span class="date">Yesterday</span>
								<span class="lnr lnr-sun condition">
									<span class="temp">23<span class="deg">0</span><span class="temp-type">C</span></span>
								</span>
							</li>
							<li>
								<span class="date">Tomorrow</span>
								<span class="lnr lnr-cloud condition">
									<span class="temp">21<span class="deg">0</span><span class="temp-type">C</span></span>
								</span>
							</li>
						</ul>
					</div>
				</div>
			</div>
		</div> -->

		<div class="col">
			<div class="weather-card">
				<div class="top">
					<div class="wrapper">
						<div class="mynav">
							<!-- <a href="javascript:;"><span class="lnr lnr-chevron-left"></span></a>
							<a href="javascript:;"><span class="lnr lnr-cog"></span></a> -->
						</div>
						<h1 class="heading">{{weather.description}}</h1>
						<h3 class="location">{{weather.location}}</h3>
						<p class="temp">
							<span class="temp-value">{{weather.temp}}</span>
							<span class="deg">0</span>
							<a href="javascript:;"><span class="temp-type">F</span></a>
						</p>
					</div>
				</div>
			</div>
		</div>
		
	</div>
</div>
</template>

<script>
    import axios from 'axios';

    export default {
        name:'test',
        data() {
            return {
                zipcode: '',
                country:'',
                weather: {
                  description:'',
                  image:'',
                  location: '',
                  temp: '',
                },

            }
        },
        
        methods: {
            pulljson: function(zip,countr){
              var self = this;
              axios.get('http://api.openweathermap.org/data/2.5/weather?zip=' + zip + ',' + countr + '&units=imperial&APPID=' + 'b3d1cfc18dcb064324b872921e0c91fc')
                .then(function(response){
                  console.log(response.data);
                  self.weather.location = response.data.name;
                  self.weather.temp = Math.round(response.data.main.temp);
                  self.weather.description = (response.data.weather["0"].description).replace(/\w\S*/g, function(txt){return txt.charAt(0).toUpperCase() + txt.substr(1).toLowerCase();});
                });
              },
                
        },
        
        mounted:function(){
          this.pulljson(78015,'us');
        }
        
    };
</script>

<style scoped>
@import url("https://fonts.googleapis.com/css?family=Montserrat:400,500,600,700,800,900");
@import url("https://cdn.linearicons.com/free/1.0.0/icon-font.min.css");

body {
  font-family: 'Montserrat', sans-serif;
  background: #112233;
}



.input-group {
    margin: 60px auto;
    width: 450px;
    box-shadow: 0 1px 38px rgba(0, 0, 0, 0.15), 0 5px 12px rgba(0, 0, 0, 0.25);
    border-radius: 0;
}

.input-group-addon {
  border-radius: 0;
}

.inputu-group-btn {
   border-radius: 0;
}

.btn {
  border-radius: 0;
}

.weather-card {
  margin: 60px auto;
  height: 570px;
  width: 450px;
  background: #fff;
  box-shadow: 0 1px 38px rgba(0, 0, 0, 0.15), 0 5px 12px rgba(0, 0, 0, 0.25);
  overflow: hidden;
}
.weather-card .top {
  position: relative;
  height: 570px;
  width: 100%;
  overflow: hidden;
  background: url("https://s-media-cache-ak0.pinimg.com/564x/cf/1e/c4/cf1ec4b0c96e59657a46867a91bb0d1e.jpg") no-repeat;
  background-size: cover;
  background-position: center center;
  text-align: center;
}
.weather-card .top .wrapper {
  padding: 30px;
  position: relative;
  z-index: 1;
}
.weather-card .top .wrapper .mynav {
  height: 20px;
}
.weather-card .top .wrapper .mynav .lnr {
  color: #fff;
  font-size: 20px;
}
.weather-card .top .wrapper .mynav .lnr-chevron-left {
  display: inline-block;
  float: left;
}
.weather-card .top .wrapper .mynav .lnr-cog {
  display: inline-block;
  float: right;
}
.weather-card .top .wrapper .heading {
  margin-top: 20px;
  font-size: 35px;
  font-weight: 400;
  color: #fff;
}
.weather-card .top .wrapper .location {
  margin-top: 20px;
  font-size: 21px;
  font-weight: 400;
  color: #fff;
}
.weather-card .top .wrapper .temp {
  margin-top: 20px;
}
.weather-card .top .wrapper .temp a {
  text-decoration: none;
  color: #fff;
}
.weather-card .top .wrapper .temp a .temp-type {
  font-size: 85px;
}
.weather-card .top .wrapper .temp .temp-value {
  display: inline-block;
  font-size: 85px;
  font-weight: 600;
  color: #fff;
}
.weather-card .top .wrapper .temp .deg {
  display: inline-block;
  font-size: 35px;
  font-weight: 600;
  color: #fff;
  vertical-align: top;
  margin-top: 10px;
}
.weather-card .top:after {
  content: "";
  height: 100%;
  width: 100%;
  display: block;
  position: absolute;
  top: 0;
  left: 0;
  background: rgba(0, 0, 0, 0.5);
}
.weather-card.rain .top {
  background: url("http://img.freepik.com/free-vector/girl-with-umbrella_1325-5.jpg?size=338&ext=jpg") no-repeat;
  background-size: cover;
  background-position: center center;
}
</style>