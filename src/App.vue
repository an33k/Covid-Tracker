<template>
<Header />
<div>
<router-view/>
</div>
  
</template>


<script>
import Header from './components/Header.vue'

export default{
  components:{
    Header,
  }
}

</script>
<style>
.front{
      display: flex;
      justify-content: center;
      padding: 2rem;
    }
</style>