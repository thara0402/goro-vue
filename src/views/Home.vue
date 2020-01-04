<template>
  <div class="home">
    <el-tabs type="card" @tab-click="handleClick">
      <el-tab-pane label="Season 1"></el-tab-pane>
      <el-tab-pane label="Season 2"></el-tab-pane>
      <el-tab-pane label="Season 3"></el-tab-pane>
      <el-tab-pane label="Season 4"></el-tab-pane>
      <el-tab-pane label="Season 5"></el-tab-pane>
      <el-tab-pane label="Season 6"></el-tab-pane>
      <el-tab-pane label="Season 7"></el-tab-pane>
    </el-tabs>
    <el-table :data="gourmets" stripe style="width: 100%">
      <el-table-column prop="episode" label="話" width="60px"></el-table-column>
      <el-table-column prop="title" label="タイトル"></el-table-column>
      <el-table-column prop="restaurant" label="店"></el-table-column>
      <el-table-column label="" width="90px">
        <template slot-scope="scope">
          <el-button @click="handleDetail(scope.row.id)">詳細</el-button>
        </template>
      </el-table-column>
    </el-table>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'
import axios from 'axios'

export default Vue.extend({
  data(){
    return {
      gourmets: []
    }
  },
  created(){
    this.getData(0)
  },
  methods:{
    getData(index:number): void{
      var season = index + 1
      axios.get("https://goro-api.azurewebsites.net/api/" + season + "/Gourmet")
      .then(response =>{
        this.gourmets = response.data
      })
      .catch(e =>{
        alert(e)
      })
    },
    handleDetail(id:string) {
      this.$router.push({ path: 'detail', query: { id: id }})
    },
    handleClick(tab:any, event:any) {
      this.getData(parseInt(tab.index))
    }    
  }
})
</script>
