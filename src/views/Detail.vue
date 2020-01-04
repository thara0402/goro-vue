<template>
  <div class="detail">
    <p>Detail</p>
    <el-form ref="form" :model="gourmet">
      <el-form-item label="シーズン" label-width="120px">
        <el-input v-model="gourmet.season" type="textbox" readonly="readonly" ></el-input>
      </el-form-item>
      <el-form-item label="話" label-width="120px">
        <el-input v-model="gourmet.episode" type="textbox" readonly="readonly"></el-input>
      </el-form-item>
      <el-form-item label="タイトル" label-width="120px">
        <el-input v-model="gourmet.title" type="textbox" readonly="readonly"></el-input>
      </el-form-item>
      <el-form-item label="店" label-width="120px">
        <el-input v-model="gourmet.restaurant" type="textbox" readonly="readonly"></el-input>
      </el-form-item>
      <el-form-item label="食べログ" label-width="120px">
        <el-input v-model="gourmet.matome" type="textbox" readonly="readonly"></el-input>
      </el-form-item>
      <el-form-item label="アクセス" label-width="120px">
        <el-input v-model="gourmet.access" type="textbox" readonly="readonly"></el-input>
      </el-form-item>
      <el-form-item label="電話番号" label-width="120px">
        <el-input v-model="gourmet.phoneNumber" type="textbox" readonly="readonly"></el-input>
      </el-form-item>
      <el-form-item label="住所" label-width="120px">
        <el-input v-model="gourmet.address" type="textbox" readonly="readonly"></el-input>
      </el-form-item>
    </el-form>
    <el-button @click="handleDetail()">戻る</el-button>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'
import axios from 'axios'

export default Vue.extend({
  data(){
    return {
      gourmet:{}
    }
  },
  created(){
    if (this.$route.query.id != null)
    {
      this.getData(this.$route.query.id as string)
    }
    else
    {
      console.log("this.$route.query.id is null.")
    }
  },
  methods:{
    getData(id:string): void{
      axios.get("https://goro-api.azurewebsites.net/api/Gourmet/" + id)
      .then(response =>{
        this.gourmet = response.data[0]
      })
      .catch(e =>{
        alert(e)
      })
    },
    handleDetail() {
      this.$router.push({ path: '/'})
    }
  }
})
</script>
