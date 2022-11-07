<template>
  <CRow>
    <CCol :xs="12">
      <CCard class="mb-4">
        <CCardHeader>
          <strong>Tabel published</strong>
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
                <CTableRow v-for="published in publisheds" :key="published.id">
                  <CTableDataCell>{{published.username}}</CTableDataCell>
                  <CTableDataCell>{{published.judul}}</CTableDataCell>
                  <CTableDataCell>{{published.tanggal}}</CTableDataCell>
                  <CTableDataCell>{{published.jenis}}</CTableDataCell>
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
    publisheds: [],
    updateSubmit: false,
  }
  },

  methods:{
    getItem() {
    axios
      .get("http://localhost:3000/published")
      .then((response) => {
        this.publisheds = response.data;
        console.log(response);
      })
      .catch(() => {
        alert("Data nya gak ada bos");
      });
  },
  },
  mounted() {
    this.getItem();
  },
}
</script>
