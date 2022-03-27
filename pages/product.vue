<template>
<div>
    <h1>สินค้า</h1>
    {{this.data}}

</div>
</template>

<script>
import axios from 'axios'
export default {
  data() {
    return {
      data: []
    };
  },
  methods: {
    async getdata(){
        await axios.get("https://fir-57331-default-rtdb.firebaseio.com/products.json")
        .then(res=>{
            this.data=res.data
            console.log(this.data);
        })
    }
  },
  mounted(){
      this.getdata()
  }
};
</script>