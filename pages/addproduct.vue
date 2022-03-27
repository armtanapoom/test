<template>
  <div>
    <b-form @submit="onSubmit(form)" @reset="onReset" v-if="show">
      <b-form-group
        id="input-group-1"
        label="ชื่อ:"
        label-for="input-1"
      >
        <b-form-input
          id="input-1"
          v-model="form.name"
          placeholder="ชื่อ"
          required
        ></b-form-input>
      </b-form-group>
      <b-form-group
        id="input-group-2"
        label="ราคา:"
        label-for="input-2"
      >
        <b-form-input
          id="input-2"
          v-model="form.price"
          placeholder="ราคา"
          required
        ></b-form-input>
      </b-form-group>
    <b-form-group
        id="input-group-3"
        label="รูป:"
        label-for="input-3"
      >
        <b-form-input
          id="input-3"
          v-model="form.pic"
          placeholder="รูป"
          required
        ></b-form-input>
      </b-form-group>
      <b-button type="submit" variant="primary">Submit</b-button>
      <b-button type="reset" variant="danger">Reset</b-button>
    </b-form>

    <b-card class="mt-3" header="Form Data Result">
      <pre class="m-0">{{ form }}</pre>
    </b-card>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  data() {
    return {
      form: {
        name: "",
        price: "",
        pic: "",
      },
      show: true,
    };
  },
  methods: {
    onSubmit(form) {
        axios.post("https://fir-57331-default-rtdb.firebaseio.com/products.json",form)
        .then(res=>{
            console.log(res);
        })
    },
    onReset(event) {
      event.preventDefault();
      // Reset our form values
      this.form.name = "";
      this.form.price = "";
      this.form.pic = "";
      // Trick to reset/clear native browser form validation state
      this.show = false;
      this.$nextTick(() => {
        this.show = true;
      });
    },
  },
};
</script>