<template>
  <div>
    <section class="teamBack" v-bind:style="styleObject">

        <div class="container">
            <div class="row">
                <div class="col-sm-3">
                    <div class="mainTeam">
                        <h1 class="mainTeam__title">
                            {{ this.About.Header_Title }}
                        </h1>
                    </div>
                </div>
            </div>
            <div class="row">
                <div class="col-sm-6">
                    <p class="mainTeam__text">
                        {{ this.About.Header_Text }}
                    </p>
                </div>
            </div>
        </div>
    </section>
    <section class="teamMain">
        <div class="container">
            <div class="row">
                <div class="col-lg-12">
                    <div class="Stories">
                        <div class="row">
                            <div class="col-lg-4">
                                <h2 class="Stories__title">
                                    {{ this.About.Block_Title }}
                                </h2>
                            </div>
                        </div>
                        <div class="row">

                            <div class="col-lg-12">
                              <p class="story">
                                {{ this.About.Block_Text }}
                              </p>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
            <div class="row">
              <div class="col-lg-12">
                <div class="teamMembers__title__block">
                  <h2 class="teamMembers__title">Наша Команда</h2>
                </div>
              </div>
              
            </div>
          <div class="row">
            <div class="col-lg-4" v-for="(member,index) in this.About.lecturers" :key="index">
              <div class="our-team-main memberColor">
              
                <div class="team-front memberColor">
                  <div class="img__block">
                    <img :src="host + member.Photo.url" class="img-fluid" />
                  </div>
                  <h4>{{ member.First_Name }} {{ member.Last_Name }}</h4>
                  <p class="member__status">
                    {{ member.position }}
                  </p>
                </div>
                
                <div class="team-back memberColor">
                  <span>
                  {{ member.info }}
                  </span>
                </div>
              
              </div>
            </div>
          </div>
        </div>
    </section>
  </div>
</template>

<script>
export default {
  name: 'study',
  data () {
    return {
      url: {
          AboutJSON: this.$store.getters.takeAbouts,
      },
      About: {},
      host: this.$store.getters.takeHost,
      styleObject: {
        color: 'red',
        fontSize: '13px',
        background: ''
      }
    }
  },

  async created () {
    const respones = await fetch(this.url.AboutJSON)
    const data = await respones.json()

    this.About = data[0]
    this.styleObject.background = 'url(' + this.host + this.About.Header_img.url + ')';
  }

}
</script>

<style scoped>
.teamBack{
    height: 600px;
    background-size: cover;
    -webkit-background-size: cover;
    -moz-background-size: cover;
    -o-background-size: cover;
}
.mainTeam{
    color: #fff;
    margin-top: 100px;
}
.mainTeam__title{
    font-family: 'Teko', sans-serif;
    font-size: 90px;
}
.mainTeam__text{
    max-width: 500px;
    font-size: 20px;
    margin-top: 20px;
    text-align: left;
    color: #000;
}
.teamMain{
    margin-top: 30px;
    margin-bottom: 80px;
}
.Stories{
    color: #fff;
    min-height: 500px;
    background: linear-gradient(0deg, #2C3846, #2C3846), linear-gradient(179.72deg, rgba(97, 139, 170, 0.44) 7.58%, rgba(58, 71, 90, 0) 99.54%);
    border-radius: 10px;
    margin-top: 100px;
    padding: 10px;
}
.Stories__title{
  color: #fff;
    font-size: 50px;
    margin-top: 30px;
}
.Stories__person{
    margin-top: 30px;
}
.Stories__person__img{
    width: 250px;
    margin-bottom: 20px;
}
.story{
  padding: 10px;
  padding-right: 20px;
  padding-left: 20px;
}
.Portfolio{
    background: linear-gradient(0deg, rgba(97, 139, 170, 0.44), rgba(97, 139, 170, 0.44)), #3D4A5B;
    min-height: 500px;
    color: #fff;
    border-radius: 10px;
    margin-top: 100px;
    padding: 10px;
}
.Portfolio__title{
    font-size: 50px;
    margin-top: 30px;
}
.company{
    margin-top: 30px;
}
.company__title{
    font-family: 'Teko', sans-serif;
    font-size: 45px;
    text-align: left;
}
.company__text{
    text-align: left;
    font-size: 15px;
}
.company__img{
    width: 250px;
}

/* Members */
.teamMembers__title__block{
  text-align: center;
  margin-top: 40px;
  margin-bottom: 30px;
}
.teamMembers__title{
  color: #fff;
}

.our-team-main
{
	width:100%;
	height:auto;
  min-height: 200px;
	background:#fff;
	text-align:center;
	border-radius:10px;
	overflow:hidden;
	position:relative;
	transition:0.5s;
	margin-bottom:28px;
  text-align: center;
}


.our-team-main img
{
	border-radius: 170px;
  width: 130px;
	margin-bottom:20px;
}

.our-team-main h3
{
  display: inline-block;
	font-size:30px;
  width: 200px;
  border-bottom: 1px #fff solid;
  padding-bottom: 8px;
}

.our-team-main p
{
	margin-bottom:0;
}

.team-back
{
	width:100%;
	height:auto;
	position:absolute;
	top:0;
	left:0;
	padding:5px 15px 0 15px;
	text-align:left;
	background:#fff;
	
}

.team-front
{
	width:100%;
	height:auto;
	position:relative;
	z-index:10;
	background:#fff;
	padding:15px;
	bottom:0px;
	transition: all 0.5s ease;
}

.our-team-main:hover .team-front
{
	bottom:-250px;
	transition: all 0.5s ease;
}

.our-team-main:hover
{
	transition:0.5s;
}
.memberColor{
  color: #fff;
  background: #618BAA;
}
</style>

