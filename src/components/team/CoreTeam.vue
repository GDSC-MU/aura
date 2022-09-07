<template>
  <v-container fluid class="py-0 my-0">
    <v-row align="center" justify="center" class="py-0 my-0">
      <v-col cols="12" md="12" lg="12" sm="12" class="py-0 my-0">
        <v-row class="team-container">
          <div>
            <v-col  v-for="(item,i) in data" :key="i">
              <CoreTeamMemberCard :data="item" />
            </v-col>
          </div>
          
        </v-row>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  name: "App",
  props: ["data"],
  components: {
    CoreTeamMemberCard: () => import("@/components/team/CoreTeamMemberCard")
  },
  data: () => ({}),
  created() {},
  methods: {}
};
</script>
<style>
  .team-container {
    overflow-x: scroll;
    align-items: center;
    scroll-behavior: smooth;
    -webkit-overflow-scrolling:auto;
    /* height: 500px; */
    /* transform: rotate(180deg); */
}
.team-container >div {
    /* transform: rotate(-180deg); */
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(350px, 1fr));
    flex-wrap: wrap;
    grid-auto-flow: column;
    grid-gap: 25px;
    height: 100%;
    text-align: center;
    justify-content: space-evenly;
    align-items: center;
    padding-bottom: 20px;
    padding-top: 20px;
    position: relative;
}

@media(min-width: 768px){
  .team-container > div {
    grid-template-rows: repeat(3, 150px);
  }
}
.lead-wrapper .team-container > div {
  grid-template-rows: 150px; 
}
.team-container .col {
    padding: 0;
    /* margin: 20px; */
    /* margin-left: 10px; */
}



</style>