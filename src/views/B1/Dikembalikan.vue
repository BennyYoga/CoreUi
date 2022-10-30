<template>
    <CRow>
      <CCol :xs="12">
        <CCard class="mb-4">
          <CCardHeader>
            <strong>Tabel Dikembalikan</strong>
          </CCardHeader>
          <CCardBody>
              <CTable>
                <CTableHead>
                  <CTableRow>
                    <CTableHeaderCell scope="col">Username</CTableHeaderCell>
                    <CTableHeaderCell scope="col">Judul</CTableHeaderCell>
                    <CTableHeaderCell scope="col">Tanggal Publish</CTableHeaderCell>
                    <CTableHeaderCell scope="col">Jenis Artikel</CTableHeaderCell>
                  </CTableRow>
                </CTableHead>
                <CTableBody>
                  <CTableRow v-for="dikembalikan in dikembalikans" :key="dikembalikan.id">
                    <CTableDataCell>{{dikembalikan.username}}</CTableDataCell>
                    <CTableDataCell>{{dikembalikan.judul}}</CTableDataCell>
                    <CTableDataCell>{{dikembalikan.tanggal}}</CTableDataCell>
                    <CTableDataCell>{{dikembalikan.jenis}}</CTableDataCell>
                  </CTableRow>
                </CTableBody>
              </CTable>
          </CCardBody>
        </CCard>
      </CCol>
    </CRow>
  </template>
  
  <script>
  import axios from "axios";
  export default {
    name: 'Tables',
    data() {
    return {
      form: {
        id: "",
        username: "",
        judul: "",
        tanggal: "",
        jenis:"",
      },
      dikembalikans: [],
      updateSubmit: false,
    }
    },

    methods:{
      getItem() {
      axios
        .get("http://localhost:3000/dikembalikan")
        .then((response) => {
          this.dikembalikans = response.data;
          console.log(response);
        })
        .catch(() => {
          alert("error");
        });
    },
    },
    mounted() {
      this.getItem();
    },
  }
  </script>
  