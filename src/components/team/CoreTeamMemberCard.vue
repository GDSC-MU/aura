<template>
    <v-dialog
      v-model="dialog"
      width="700"
    >
      <template v-slot:activator="{ on }">
          <div v-on="on" style="cursor: pointer;" class="core-card" :class="$vuetify.theme.dark == true?'darkModeCard':'whiteTheme'" >
               <v-avatar class="core-team-img" size="100">
                  <img 
                    :src="getImgUrl(data.image, 'profile.jpg')"
                    :lazy-src="getImgUrl(data.image, 'profile.jpg')" alt=""
                  >
                </v-avatar>
                <div class="core-team-card-info">
                  <socialMediaDetails :data="data.socialLinks" class="social"/>
                  <div>
                    <p class="mt-3 mb-0 google-font mb-0" style="font-size:120%">{{data.name | summery(20)}}</p>
                    <p class="mt-1 mb-0 google-font mt-0" style="font-size:80%">{{data.designation | summery(20)}}</p>
                  </div>
              </div>
          </div>
          
      </template>

      <v-card :class="theme.isDark?'grey darken-3':'white'">
        <v-card-title
          class="px-5 google-font"
          primary-title
        >
         {{data.name}} 
        </v-card-title>

        <v-card-text class="pa-5">
            <p class="google-font">{{data.designation}}</p>
            <p class="google-font">{{data.bio}}</p>
            
            <socialMediaDetails  class="pl-0 ml-0" :data="data.socialLinks"/>

            <v-btn class="primary mt-3" small depressed @click="goToTeam(data.id)">See More Info</v-btn>
        </v-card-text>

        <v-divider></v-divider>

        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn
            color="primary"
            text
            @click="dialog = false"
          >
            Close
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
</template>

<script>
import socialMediaDetails from '@/components/common/SocialInfo'
  export default {
    components:{
        socialMediaDetails
    },
    inject: ['theme'],
    props:['data'],
    data () {
      return {
        dialog: false,
      }
    },
    mounted(){
     
    },
    methods:{
      goToTeam(id){
        this.$router.push("/team/" + id);
      },
    },
    filters:{
        summery: (val,num)=>{
          if(val.length > num)
            return val.substring(0,num)+".."
          else
            return val;
        }
    }
  }
</script>
<style>
.core-card {
    display: flex;
    justify-content: space-around;
    align-items: center;
    height: 150px;
    width: 350px;
    position: relative;
}

.core-card::after {
    content: "";
    width: 100%;
    position: absolute;
    height: 1px;
    background-color: #dfdfdf;
    z-index: 1;
    top: 40%;
    left: 0;
}

.core-team-img {
    position: relative;
    z-index: 2;
    border: solid 1px #dfdfdf;
    position: absolute !important;
    top: 50%;
    transform: translateY(-50%);
    left: 30px;
}
.core-team-card-info {
    position: absolute;
    right: 0px;
    height: 100%;
    width: 200px;
    display: flex;
    justify-content: end;
    align-items: center;
    flex-direction: column;
}
.core-team-card-info > div {
    margin-bottom: 25px;
}
.core-team-card-info .social {
    position: absolute;
    top: 30px;
    width: 100%;
}
</style>