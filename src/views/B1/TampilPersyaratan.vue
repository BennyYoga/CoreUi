<template>
  <CButton color="primary" @click="() => { visibleTop = !visibleTop }">+ Tambah</CButton>
  <COffcanvas placement="top" :visible="visibleTop" @hide="() => { visibleTop = !visibleTop }">
    <CRow>
    <CCol :xs="12">
      <CCard class="mb-4">
        <CCardHeader>
          <strong>Persyaratan</strong>
        </CCardHeader>
        <CCardBody>
            <form @submit.prevent="PostItem">
              <div class="mb-3">
                <CFormLabel for="exampleFormControlInput1">ID</CFormLabel>
                <CFormInput v-model="form.id" type="text" placeholder="" aria-label="Id"/>
              </div>
              <div class="mb-3">
                <CFormLabel for="exampleFormControlInput1">Nama Persyaratan</CFormLabel>
                <CFormInput v-model="form.name" type="text" placeholder="" aria-label="Nama Persyaratan"/>
              </div>
              <div class="mb-3">
                <CFormLabel for="exampleFormControlTextarea1">Tipe Data</CFormLabel>
                <CFormSelect v-model="form.tipeData"
                aria-label="Default select example"
                :options="[
                  'Pilih Tipe Data',
                  { label: 'String', value: '1' },
                  { label: 'Integer', value: '2' },
                  { label: 'Date', value: '3'}
                ]">
              </CFormSelect>
              </div>
              <div class="mb-3">
                <CFormLabel  v-model="form.length" for="exampleFormControlInput1">Lenght</CFormLabel>
                <CFormInput type="text" placeholder="" aria-label="Lenght"/>
              </div>
              <div class="mb-3">
                <CButton type="submit" v-show="!updateSubmit" name="submit" color="light">Save</CButton>
              </div>
            </form>
        </CCardBody>
      </CCard>
    </CCol>
    
  </CRow>
  </COffcanvas>
  <p></p>
    <CRow>
      <CCol :xs="12">
        <CCard class="mb-4">
          <CCardHeader>
            <strong>Tabel Persyaratan</strong>
          </CCardHeader>
          <CCardBody>
              <CTable>
                <CTableHead>
                  <CTableRow>
                    <CTableHeaderCell scope="col">Nama Persyaratan</CTableHeaderCell>
                    <CTableHeaderCell scope="col">Tipe Data</CTableHeaderCell>
                    <CTableHeaderCell scope="col">Length</CTableHeaderCell>
                    <CTableHeaderCell scope="col"></CTableHeaderCell>
                    <CTableHeaderCell scope="col"></CTableHeaderCell>
                  </CTableRow>
                </CTableHead>
                <CTableBody>
                  <CTableRow v-for="persyaratan in persyaratans" :key="persyaratan.id">
                    <CTableDataCell>{{ persyaratan.namaPersyaratan }}</CTableDataCell>
                    <CTableDataCell>{{ persyaratan.tipeData }}</CTableDataCell>
                    <CTableDataCell>{{ persyaratan.length}}</CTableDataCell>
                    <CTableDataCell><CButton  v-on:click="Edit(user)" color="light">Edit</CButton> <CButton v-on:click="Delete(user)" color="light">Delete</CButton></CTableDataCell>
                  </CTableRow>
                </CTableBody>
              </CTable>
          </CCardBody>
        </CCard>
      </CCol>
    </CRow>
  </template>
  
  <script>
  //json-server --watch db.json
  import axios from "axios";
  export default {
    name: 'Tables',
    data() {
      return { 
        visibleTop: false,
        form: {
        id: "",
        namaPersyaratan: "",
        tipeData:"",
        length:"",
        },
        persyaratans: [],
        updateSubmit: false,
      }
    },
    methods: {
    getItem(){
      axios
        .get("http://localhost:3000/persyaratan")
        .then((response) => {
          this.persyaratans = response.data;
          console.log(response);
        })
        .catch(() => {
          alert("error");
        });
    }
    },
    mounted(){
      this.getItem();
    },

    PostItem() {
      axios
        .post("http://localhost:3000/persyaratan", this.form)
        .then(() => {
          this.getItem();
          this.form.id = "";
          this.form.namaPersyaratan = "";
          this.form.tipeData = "";
          this.form.length = "";
          alert("saved...");
        })
        .catch((err) => {
          console.log(err);
          alert("saving  error");
        });
    },

    Edit(persyaratan) {
      this.updateSubmit = true;
      this.form.id = persyaratan.id;
      this.form.namaPersyaratan = persyaratan.namaPersyaratan;
      this.form.tipeData = persyaratan.tipeData;

    },

    Update(form) {
      axios
        .put(`http://localhost:3000/persyaratan/${form.id}`, {
          name: this.form.namaPersyaratan,
        })
        .then(() => {
          this.getItem();
          this.form.id = "";
          this.form.namaPersyaratan = "";
          this.form.tipeData = "";
          this.form.length = "";
          this.updateSubmit = false;
          alert("updated...");
        })
        .catch((err) => {
          console.log(err);
          console.warn();
          alert("Error...");
        });
    },
    Delete(persyaratan) {
      axios
        .delete("http://localhost:3000/persyaratan/" + persyaratan.id)
        .then(() => {
          this.getItem();
          this.form.namaPersyaratan = "";
          alert("Deleted...");
        })
        .catch((err) => {
          console.log(err);
        });
    },

  };
  //func
  
  </script>
  