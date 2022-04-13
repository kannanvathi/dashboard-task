<template>
  <b-container fluid>
    <!-- User Interface controls -->
    <b-row class="pt-3 pb-3">
      <b-col sm="12" md="6" lg="3">
        <b-card>
          <div class="box approval-pending">
            <span class="count">12</span>
            <p class="text">Approval pending</p>
          </div>
        </b-card>
      </b-col>
      <b-col sm="12" md="6" lg="3">
        <b-card>
          <div class="box cancel-booking">
            <span class="count">07</span>
            <p class="text">Cancel Booking</p>
          </div>
        </b-card>
      </b-col>
      <b-col sm="12" md="6" lg="3">
        <b-card>
          <div class="box canceling">
            <span class="count">10</span>
            <p class="text">Canceling</p>
          </div>
        </b-card>
      </b-col>
      <b-col sm="12" md="6" lg="3">
        <b-card>
          <div class="box refund-initiated">
            <span class="count">08</span>
            <p class="text">Refund initiated</p>
          </div>
        </b-card>
      </b-col>
    </b-row>
    <b-row class="mb-2">
      <b-col lg="6">
        <p class="med-text mb-0">List of Contents</p>
      </b-col>
      <b-col sm="12" lg="6" class="my-1">
        <div class="d-flex align-items-center justify-content-end w-100">
        <div class="d-flex align-items-center justify-content-start mr-3">
          <label class="label">Search:</label>
          <b-form-input
            id="filter-input"
            v-model="filter"
            type="search"
            placeholder="Type to Search"
          >
          </b-form-input>
        </div>
        <div class="d-flex align-items-center justify-content-start">
          <label class="label">Records Per page</label>
          <b-form-select
            id="per-page-select"
            v-model="perPage"
            :options="pageOptions"
            size="sm"
          >
          </b-form-select>
        </div>
        </div>
      </b-col>
    </b-row>

    <!-- Main table element -->
    <b-table
      :items="items"
      :fields="fields"
      :current-page="currentPage"
      :per-page="perPage"
      :filter="filter"
      :filter-included-fields="filterOn"
      :sort-by.sync="sortBy"
      :sort-desc.sync="sortDesc"
      :sort-direction="sortDirection"
      stacked="md"
      show-empty
      small
      @filtered="onFiltered"
    >
      <template #cell(booking_date)="row">
        {{ row.value }}
      </template>

      <template #cell(actions)="row">
        <a size="sm" @click="info(row.item, row.index, $event.target)" class="mr-1">
          <i class="fa-solid fa-eye"></i>
        </a>
      </template>

      <template #row-details="row">
        <b-card>
          <ul>
            <li v-for="(value, key) in row.item" :key="key">{{ key }}: {{ value }}</li>
          </ul>
        </b-card>
      </template>
    </b-table>

    <b-row>
        <b-col sm="12" md="6">

        </b-col>
        <b-col sm="12" md="6" class="my-1">
          <b-pagination
            v-model="currentPage"
            :total-rows="totalRows"
            :per-page="perPage"
            align="fill"
            size="sm"
            class="my-0 mb-2"
          ></b-pagination>
        </b-col>
    </b-row>
    <!-- Info modal -->
    <b-modal :id="infoModal.id" :title="infoModal.title" ok-only @hide="resetInfoModal">
      <pre>{{ infoModal.content }}</pre>
    </b-modal>
  </b-container>
</template>

<script>
  import { BCard, BRow, BCol, BContainer, BFormCheckbox, BFormCheckboxGroup, BFormInput, BButton, BBadge, BFormSelect, BTable, BPagination, BModal, BForm, BFormGroup, BInputGroup, BInputGroupAppend, BAlert} from 'bootstrap-vue'
    export default {
        name: "ContentComponent",
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
          items: [
            { house: 'High Road House', confirmation_no: 100092343, booking_date: '10/02/2022', first_name: 'John', last_name: 'Christopher', contact_number: '+91 972343234', status:  'Approval pending', _cellVariants: { status: 'warning' } },
            { house: 'xxx House', confirmation_no: 100092341, booking_date: '10/02/2022', first_name: 'John', last_name: 'Christopher', contact_number: '+91 972343234', status:  'Approval pending', _cellVariants: { status: 'warning' } },
            {
              house: 'yyy House',
              confirmation_no: 9,
              booking_date: '10/02/2022'
              , first_name: 'John', last_name: 'Christopher', contact_number: '+91 972343234', status:  'Approval pending', _cellVariants: { status: 'warning' }

            },
            { house: 'zzz House', confirmation_no: 100092342, booking_date: '10/02/2022', first_name: 'John', last_name: 'Christopher', contact_number: '+91 972343234', status:  'Canceling', _cellVariants: { status: 'danger' } },
            { house: 'xxx House', confirmation_no: 100092343, booking_date: '10/02/2022', first_name: 'John', last_name: 'Christopher', contact_number: '+91 972343234', status:  'Approval pending', _cellVariants: { status: 'warning' } },
            { house: 'xxx House', confirmation_no: 100092343, booking_date: '10/02/2022', first_name: 'Cart', last_name: 'Christopher', contact_number: '+91 972343234',  status:  'Canceling', _cellVariants: { status: 'danger' } },
            { house: 'xxx House', confirmation_no: 100092343, booking_date: '10/02/2022', first_name: 'John', last_name: 'Christopher', contact_number: '+91 972343234', status:  'Approval pending', _cellVariants: { status: 'warning' }},
            {
              house: 'xxx House',
              confirmation_no: 100092343,
              booking_date: '10/02/2022',
            first_name: 'John', last_name: 'Christopher', contact_number: '+91 972343234', status:  'Approval pending',
              _cellVariants: { status: 'warning' }
            },
            { house: 'xxx House', confirmation_no: 100092343, booking_date: '11/02/2022', first_name: 'John', last_name: 'Christopher', contact_number: '+91 672343234', status:  'Approval pending', _cellVariants: { status: 'warning' } },
            { house: 'xxx House', confirmation_no: 100092343, booking_date: '12/02/2022', first_name: 'William', last_name: 'Christopher', contact_number: '+91 9723433434',  status:  'Canceling', _cellVariants: { status: 'danger' } },
            { house: 'xxx House', confirmation_no: 1000923421, booking_date: '13/02/2022', first_name: 'John', last_name: 'Christopher', contact_number: '+91 9723432232', status:  'Approval pending', _cellVariants: { status: 'warning' } },
            { house: 'xxx House', confirmation_no: 1000923234, booking_date: '14/02/2022', first_name: 'William', last_name: 'Christopher', contact_number: '+91 972343233', status:  'Approval pending', _cellVariants: { status: 'warning' } }
          ],
          fields: [
            { key: 'booking_date', label: 'Booking Date', sortable: true, sortDirection: 'desc' },
            { key: 'confirmation_no', label: 'Confirmation Number', sortable: true, class: 'text-center' },
            {key: 'first_name', label: 'First Name', sortable: true, sortDirection: 'desc'},
            {key: 'last_name', label: 'Last Name', sortable: true, sortDirection: 'desc'},
            {key: 'contact_number', label: 'Contact Number', sortable: true, sortDirection: 'desc'},
            {key: 'status', label: 'Status', sortable: true, sortDirection: 'desc'},
            {
              key: 'house',
              label: 'House',
              sortable: true,
              sortByFormatted: true,
              filterByFormatted: true
            },
            { key: 'actions', label: 'Actions' }
          ],
          totalRows: 1,
          currentPage: 1,
          perPage: 10,
          pageOptions: [10, 15, { value: 100, text: "Show a lot" }],
          sortBy: '',
          sortDesc: false,
          sortDirection: 'asc',
          filter: null,
          filterOn: [],
          infoModal: {
            id: 'info-modal',
            title: '',
            content: ''
          }
        }
      },
      computed: {
        sortOptions() {
          // Create an options list from our fields
          return this.fields
            .filter(f => f.sortable)
            .map(f => {
              return { text: f.label, value: f.key }
            })
        }
      },
      mounted() {
        // Set the initial number of items
        this.totalRows = this.items.length
      },
      methods: {
        info(item, index, button) {
          this.infoModal.title = `Row index: ${index}`
          this.infoModal.content = JSON.stringify(item, null, 2)
          this.$root.$emit('bv::show::modal', this.infoModal.id, button)
        },
        resetInfoModal() {
          this.infoModal.title = ''
          this.infoModal.content = ''
        },
        onFiltered(filteredItems) {
          // Trigger pagination to update the number of buttons/pages due to filtering
          this.totalRows = filteredItems.length
          this.currentPage = 1
        }
      }
    }

</script>

<style scoped>


  .box{
    width: 100%;
    height: 158px;
    border-radius: 15px;
    position: relative;
  }
 .box .count{
   font-size: 38px;
   line-height: 70px;
   padding-left: 15px;
   padding-top: 15px;
   color: #fff;
 }
 .box .text{
   font-size: 12px;
   color: #fff;
   position: absolute;
   left: 15px;
   bottom: 5px;
 }
  .box{
    background-size: cover;
    background-position: center;
    background-repeat: no-repeat;
  }
 .box.approval-pending{
   background-image: url("../../src/assets/images/card-1.png");
   background-size: cover;
   background-position: center;
   background-repeat: no-repeat;
 }
  .box.cancel-booking{
    background: url("../../src/assets/images/card-2.png");
    background-size: cover;
    background-position: center;
    background-repeat: no-repeat;
  }
  .box.canceling{
    background: url("../../src/assets/images/card-3.png");
    background-size: cover;
    background-position: center;
    background-repeat: no-repeat;
  }
  .box.refund-initiated{
    background: url("../../src/assets/images/card-4.png");
    background-size: cover;
    background-position: center;
    background-repeat: no-repeat;
  }
  .card{
    background: transparent !important;
    border: none !important;
  }
  input[type=search] {
    min-width: 150px;
  }
  .label{
    font-size: 12px;
    margin-right: 5px;
    margin-bottom: 0;
  }
  ::placeholder{
    font-size: 12px;
  }

</style>

<style>

  .page-item.active .page-link {
    z-index: 2;
    color: #162b43;
    background-color: #f1f1f1;
    background-image: linear-gradient(#ededed, #dadada);
    /* border-color: #dedede; */
    -moz-box-shadow: inset 0 0 10px #000000;
    /* -webkit-box-shadow: inset 0 0 10px #000000; */
    /* box-shadow: inset 0 0 10px #d0d0d0; */
    border-radius: 3px;
    border-color: #dedede;
  }
  button:focus{
    outline: none;
  }
  .page-link {
    position: relative;
    display: block;
    padding: 0.5rem 0.75rem;
    margin-left: -1px;
    line-height: 1.25;
    color: #162b43;
    background-color: transparent;
    border: 1px solid transparent;
  }
  .pagination-sm .page-link {
    padding: 10px 10px;
    font-size: .875rem;
  }
  .pagination-sm .page-link {
    padding: 10px 10px;
    font-size: .875rem;
  }
  .page-item.disabled .page-link {
    color: #636c72;
    pointer-events: none;
    cursor: not-allowed;
    background-color: transparent;
    border-color: transparent;
  }
  .b-pagination.pagination-sm{
    float: right;
    margin-right: 15px;
  }
  .b-table{
    font-size: 12px;
  }
  .container-fluid{
    max-height: calc(100% - 120px) !important;
    overflow-y: scroll;
  }
  .table thead th{
    background: #d6d6d6;
  }
  .table-sm td, .table-sm th{
    padding: 10px;
  }
  .table-warning div{
    padding: 7px;
    border-radius: 15px;
    color: #e3b858;
    border: 1px solid #e3b858;
    background: #fff3df;
    text-align: center;
  }
  .table-danger div{
    padding: 7px;
    border-radius: 15px;
    color: #f99181;
    border: 1px solid #f99181;
    background: #ffded9;
    text-align: center;
  }
  .table-danger, .table-danger>td, .table-danger>th, .table-warning, .table-warning>td, .table-warning>th{
    background: transparent;
  }
  .med-text{
    line-height: 40px;
  }
  .table td{
    background: #fff;
  }
</style>
