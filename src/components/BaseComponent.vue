<template>
  <b-container class="bv-example-row">
    <b-row>
      <b-col
        lg="6"
        md="6"
        sm="12"
      ><form-component
        @getDetails = 'getDetails'
      />
      </b-col>

      <b-col
        lg="6"
        md="6"
        sm="12"
      >
        <!--<table-component />-->
        <b-table
          responsive="sm"
          striped hover :items="details">

          <template #cell(actions)="data">
            <>
          </template>
        </b-table>
      </b-col>

    </b-row>
  </b-container>
</template>

<script>
    import FormComponent from "./FormComponent";
    import TableComponent from "./TableComponent";
    import { BCard, BRow, BCol, BContainer, BFormCheckbox, BFormCheckboxGroup, BFormInput, BButton, BBadge, BFormSelect, BTable, BPagination, BModal, BForm, BFormGroup, BInputGroup, BInputGroupAppend, BAlert} from 'bootstrap-vue'
    export default {
        name: "BaseComponent",
      components: {
          TableComponent,
        FormComponent,
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
          details: [
            {'first_name': 'xxx', 'last_name': 'yyy', 'email': 'aa@gmail.com'}
            ],
        }
      },
      methods: {
          getDetails(details) {
            this.details.push(details);
            console.log(this.details);
          }
      }
    }
</script>

<style scoped>

</style>
