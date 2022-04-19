<template>
  <b-container>
  <b-form
    @submit.prevent="onSubmit"
  >
    <b-form-group
      label="First Name"
      label-for="first_name"
    >
      <b-form-input
        id="first_name"
        v-model="form.first_name"
        type="text"
        placeholder="Enter First name"
        required
      ></b-form-input>
    </b-form-group>
    <b-form-group
      label="Last Name"
      label-for="last_name"
    >
      <b-form-input
        id="last_name"
        v-model="form.last_name"
        type="text"
        placeholder="Enter Last name"
        required
      ></b-form-input>
    </b-form-group>
    <b-form-group
      id=""
      label="Email Address"
      label-for="email"
    >
      <b-form-input
        id="email"
        v-model="form.email"
        type="email"
        placeholder="Enter Email"
        required
      ></b-form-input>
    </b-form-group>
    <div class="mt-3">
      <button class="btn btn-primary" type="submit">Submit</button>
      <button class="btn btn-secondary" @click="onReset">Reset</button>
    </div>
</b-form>
  </b-container>
</template>

<script>
  import { BCard, BRow, BCol, BContainer, BFormCheckbox, BFormCheckboxGroup, BFormInput, BButton, BBadge, BFormSelect, BTable, BPagination, BModal, BForm, BFormGroup, BInputGroup, BInputGroupAppend, BAlert} from 'bootstrap-vue'
    export default {
        name: "FormComponent",
      components: {
        BContainer,
        BFormCheckbox,
        BFormCheckboxGroup,
        BCard,
        BRow,
        BCol,
        BFormSelect,
        BFormInput,
        BButton,
        BBadge,
        BTable,
        BPagination,
        BModal,
        BForm,
        BFormGroup,
        BInputGroup,
        BInputGroupAppend,
        BAlert
      },
      data() {
          return {
            form: {
              first_name: '',
              last_name: '',
              email: ''
            },
            details: [],
          }
      },
      methods: {
          onSubmit() {
            this.$emit('getDetails', {
              'first_name' : this.form.first_name,
              'last_name' : this.form.last_name,
              'email' : this.form.email,
            });
            this.onReset();
          },
          onReset() {
            this.form.first_name = '';
            this.form.last_name = '';
            this.form.email = '';

          }
      }



    }
</script>

<style scoped>

</style>
