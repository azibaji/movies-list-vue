<template>
    <div class="header">
      <div>
        <label>Search by release date:</label>
        <input type="date" v-model="dateInput"/>
      </div>
      
      <button @click="searchMovieByDate"> search</button>

    </div>
</template>
<script>
export default {
    data:()=>({
        dateInput:'2018-07-22'
    }),
    methods:{
        searchMovieByDate(){
            this.$emit('searchMovieByDate', this.dateInput)
        }
    }
}
</script>
<style lang="scss" scoped>
  .header{
      background: #E2E2E2;
      border-radius: 6px;
      display: flex;
      justify-content: space-between;
      padding: 18px 80px;
      margin-bottom: 78px;
      align-items: center;
      label{
        margin-right:24px;
        font-weight: 400;
        font-size: 16px;
        line-height: 19px;
      }
      input{
        border: 1px solid #CFCFCF
      }
      button{
         background: #549DF2;
         border-radius: 100px;
         color: white;
         align-self: center;
         padding: 7px 14px;
         text-decoration: none;
         border:0px;
      }
  }
</style>