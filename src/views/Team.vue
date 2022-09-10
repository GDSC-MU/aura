<template>
    <v-content class="px-0 mx-1">
      <v-container fluid class="pa-0">
             <v-row justify="center" align="center" class="py-3" :class="this.$vuetify.theme.dark == true?'grey darken-4':'grey lighten-4'" >
                <v-col md="12" lg="10" sm="11" xs="12" class="pt-3 bottom-space"  >
                  <TeamHeader :data="lead" />
                </v-col>
             </v-row>
        </v-container>

        <v-container fluid class="pa-0">
             <v-row justify="center" align="center" class="py-3" :class="this.$vuetify.theme.dark == true?'black':''">
                <v-col md="12" lg="10" sm="11" xs="12" class="lead-wrapper pt-3 card-top-margin" v-if="Leads.length>0"  >
                  <CoreTeam :data="Leads"/>
                </v-col>
                <v-col v-if="loader" md="12" lg="10" xs="12" class="pt-3 card-top-margin"  >
                  <v-container fluid class="">
                      <v-row >
                          <v-col md="2" lg="2" sm="3" cols="6" v-for="i in 6" :key="i">
                                <v-sheet
                                    :color="`grey ${theme.isDark ? 'darken-2' : 'lighten-4'}`"
                                    class=""
                                >
                                    <v-skeleton-loader
                                    class="mx-auto"
                                    max-width="300"
                                    type="card"
                                    ></v-skeleton-loader>
                                </v-sheet>
                            </v-col>
                      </v-row>
                  </v-container>
                </v-col>
             </v-row>
        </v-container>
        <v-container fluid class="pa-0">
             <v-row justify="center" align="center" class="py-3"  >
                <v-col md="12" lg="10" sm="11" xs="12" class="pt-3 bottom-space"  >
                  <TeamHeader :data="current" />
                </v-col>
             </v-row>
        </v-container>

        <v-container fluid class="pa-0">
             <v-row justify="center" align="center" class="py-3" :class="this.$vuetify.theme.dark == true?'black':''">
                <v-col md="12" lg="10" sm="11" xs="12" class="pt-3 card-top-margin" v-if="CoreTeamCurrent.length>0"  >
                  <CoreTeam :data="CoreTeamCurrent"/>
                </v-col>
                <v-col v-if="loader" md="12" lg="10" xs="12" class="pt-3 card-top-margin"  >
                  <v-container fluid class="">
                      <v-row >
                          <v-col md="2" lg="2" sm="3" cols="6" v-for="i in 6" :key="i">
                                <v-sheet
                                    :color="`grey ${theme.isDark ? 'darken-2' : 'lighten-4'}`"
                                    class=""
                                >
                                    <v-skeleton-loader
                                    class="mx-auto"
                                    max-width="300"
                                    type="card"
                                    ></v-skeleton-loader>
                                </v-sheet>
                            </v-col>
                      </v-row>
                  </v-container>
                </v-col>
             </v-row>
        </v-container>
        <v-container fluid class="pa-0">
             <v-row justify="center" align="center" class="py-3"  >
                <v-col md="12" lg="10" sm="11" xs="12" class="pt-3 bottom-space"  >
                  <TeamHeader :data="previous" />
                </v-col>
             </v-row>
        </v-container>

        <v-container fluid class="pa-0 add-margin-bottom">
             <v-row justify="center" align="center" class="py-3" :class="this.$vuetify.theme.dark == true?'black':''">
                <v-col md="12" lg="10" sm="11" xs="12" class="pt-3 card-top-margin" v-if="CoreTeamPrevious.length>0"  >
                  <CoreTeam :data="CoreTeamPrevious"/>
                </v-col>
                <v-col v-if="loader" md="12" lg="10" xs="12" class="pt-3 card-top-margin"  >
                  <v-container fluid class="">
                      <v-row >
                          <v-col md="2" lg="2" sm="3" cols="6" v-for="i in 6" :key="i">
                                <v-sheet
                                    :color="`grey ${theme.isDark ? 'darken-2' : 'lighten-4'}`"
                                    class=""
                                >
                                    <v-skeleton-loader
                                    class="mx-auto"
                                    max-width="300"
                                    type="card"
                                    ></v-skeleton-loader>
                                </v-sheet>
                            </v-col>
                      </v-row>
                  </v-container>
                </v-col>
             </v-row>
        </v-container>
        <v-container fluid class="pa-0" v-if="OrganizingTeam.length>0">
             <v-row justify="center" align="center" class="py-3">
                <v-col md="12" lg="10" sm="11" xs="12" class="pt-3 ">
                  <OrgainizingTeam :data="OrganizingTeam"/>
                </v-col>
             </v-row>
        </v-container>
        <v-container fluid class="pa-0">
             <v-row justify="center" align="center" class="py-3" :class="this.$vuetify.theme.dark == true?'black':''">
               <v-col v-if="!loader && notFound && OrganizingTeam.length <=0 && CoreTeamCurrent.length<=0" md="12" lg="12" sm="12" cols="12" class="text-center">
                <v-img
                  :src="require('@/assets/img/svg/DataNotFound.svg')"
                  :lazy-src="require('@/assets/img/svg/DataNotFound.svg')"
                  width="15%"
                  style="border-radius:8px;margin-left:auto;margin-right:auto"
                >
                  <template v-slot:placeholder>
                    <v-row class="fill-height ma-0" align="center" justify="center">
                      <v-progress-circular indeterminate color="grey lighten-5"></v-progress-circular>
                    </v-row>
                  </template>
                </v-img>
                <h2 class="google-font">Team Not Found</h2>
              </v-col>
             </v-row>
        </v-container>

    </v-content>

</template>

<script>
import service from '@/services/appservices'
export default {
    name:'Team',
    inject: ['theme'],
    components:{
        TeamHeader:()=>import('@/components/team/TeamHeader'),
        CoreTeam:()=>import('@/components/team/CoreTeam'),
        OrgainizingTeam:()=>import('@/components/team/OrganizingTeam')
    },
    data:() =>({
      loader:true,
      OrganizingTeam:[],
      CoreTeamCurrent:[],
      CoreTeamPrevious:[],
      Volunteers:[],
      Leads: [],
      notFound:false,
      ErrorMsg:'',
      current: {title:"Current Team"},
      previous: {title:"Previous Team"},
      lead:{title: "Leads"}
    }),
    mounted(){
        this.getAllTeamMembers();
        console.log(this.CoreTeamCurrent);
    },
    methods:{
        getAllTeamMembers(){
          this.loader = true
          service.getTeam().then(res=>{
            if(res.success==true){
              this.OrganizingTeam = res.data.filter(res=>res.role=='Organizing Team' && res.visible );
              this.CoreTeamCurrent = res.data.filter(res=>res.role=='Core Team' && res.visible && res.active && !res.designation.toLowerCase().includes("lead"));
              this.Leads = res.data.filter(res=>res.role=='Core Team' && res.visible  && res.designation.toLowerCase().includes("lead"));
              this.CoreTeamPrevious = res.data.filter(res=>res.role=='Core Team' && res.visible && !res.active && !res.designation.toLowerCase().includes("lead"));
              this.Volunteers = res.data.filter(res=>res.role=='Volunteer' && res.visible );
              this.loader = false
              this.notFound = false
            }else{
              this.notFound = true
              this.loader = false
            }
          }).catch(e=>{
            this.loader = false
            this.notFound = true
            this.ErrorMsg = e
          })
        }
    }

}
</script>

<style scoped>
  .darkbg{
    /* background: #1F1A24 */
  }
  .add-margin-bottom {
    margin-bottom: 40px !important;
  }
  @media screen and (min-width: 600px) {
    .card-top-margin {
      margin-top:-110px
    }
    .bottom-space{
      margin-bottom: 80px;
      margin-top: 20px
    }
  }
  @media screen and (max-width: 600px) {
    .card-top-margin {
      margin-top:-100px
    }
    .bottom-space{
      margin-bottom: 50px
    }
  }
</style>