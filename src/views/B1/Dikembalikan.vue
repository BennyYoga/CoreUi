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
                    <CTableHeaderCell scope="col">ID</CTableHeaderCell>
                    <CTableHeaderCell scope="col">Judul</CTableHeaderCell>
                    <CTableHeaderCell scope="col">Deskripsi</CTableHeaderCell>
                    <CTableHeaderCell scope="col">Waktu Terbit</CTableHeaderCell>
                  </CTableRow>
                </CTableHead>
                <CTableBody>
                  <CTableRow v-for="dikembalikan in dikembalikans" :key="dikembalikan.id_status_artikel">
                    <CTableDataCell>{{dikembalikan.id_artikel}}</CTableDataCell>
                    <CTableDataCell>{{dikembalikan.judul_artikel}}</CTableDataCell>
                    <CTableDataCell>{{dikembalikan.deskripsi_artikel}}</CTableDataCell>
                    <CTableDataCell>{{dikembalikan.waktu_terbit}}</CTableDataCell>
                    <CTableDataCell>
                      <CButton v-on:click="Edit(persyaratan.id)" color="light">Tolak</CButton> <CButton v-on:click="Delete(persyaratan.id_persyaratan)" color="light">Terima</CButton>
                    </CTableDataCell>
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
        id_artikel: "",
        id_user: "",
        id_status_artikel: "",
        id_tag: "",
        deskripsi_artikel:"",
        isi_artikel:"",
        judul_artikel:"",
        waktu_terbit:"",
      },
      dikembalikans: [],
      updateSubmit: false,
    }
    },

    methods:{
      getItem() {
      axios
        .get("http://localhost:3010/artikel/editor/inreview")
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
  