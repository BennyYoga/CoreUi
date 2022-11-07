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
            <form v-on:submit.prevent="PostItem">
              <div class="mb-3">
                <CFormLabel for="exampleFormControlInput1">Id Persyaratan</CFormLabel>
                <CFormInput v-model="form.id_persyaratan" type="text" placeholder="" aria-label="Id Persyaratan" />
              </div>
              <div class="mb-3">
                <CFormLabel for="exampleFormControlInput1">Nama Persyaratan</CFormLabel>
                <CFormInput v-model="form.nama_persyaratan" type="text" placeholder="" aria-label="Nama Persyaratan" />
              </div>
              <div class="mb-3">
                <CFormLabel for="exampleFormControlTextarea1">Id Jenis Persyaratan</CFormLabel>
                <CFormSelect v-model="form.id_jenis_persyaratan" aria-label="Default select example" :options="[
                  'Pilih Id Persyaratan',
                  { label: 'File', value: '1' },
                  { label: 'Gambar', value: '2' },
                  { label: 'Teks', value: '3' }
                ]">
                </CFormSelect>
              </div>
              <div class="mb-3">
                <CFormLabel for="exampleFormControlInput1">Deskripsi</CFormLabel>
                <CFormInput v-model="form.deskripsi_persyaratan" type="text" placeholder="" aria-label="Lenght" />
              </div>
              <div class="mb-3">
                <CButton type="submit" color="light">submit</CButton>
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
                <CTableHeaderCell scope="col">Deskripsi</CTableHeaderCell>
                <CTableHeaderCell scope="col"></CTableHeaderCell>
                <CTableHeaderCell scope="col"></CTableHeaderCell>
              </CTableRow>
            </CTableHead>
            <CTableBody>
              <CTableRow v-for="persyaratan in persyaratans" :key="persyaratan.id_persyaratan">
                <CTableDataCell>{{ persyaratan.nama_persyaratan }}</CTableDataCell>
                <CTableDataCell>{{ persyaratan.deskripsi_persyaratan }}</CTableDataCell>
                <CTableDataCell>
                  <CButton v-on:click="Edit(persyaratan.id)" color="light">Edit</CButton> <CButton v-on:click="Delete(persyaratan.id_persyaratan)" color="light">Delete</CButton>
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
//json-server --watch db.json
import axios from "axios";
export default {
  name: 'Tables',
  data() {
    return {
      visibleTop: false,
      form: {
        id_persyaratan: "",
        id_jenis_persyaratan: "",
        nama_persyaratan: "",
        deskripsi_persyaratan: "",
        stuatus_persyaratan: "",
      },
      persyaratans: [],
      updateSubmit: false,
    }
  },
  methods: {
    getItem() {
      axios
        .get("http://localhost:3000/admin/persyaratan")
        .then((response) => {
          this.persyaratans = response.data;
          console.log(response);
        })
        .catch(() => {
          alert("Data Tidak Ada Boss");
        });
    },
    check : function(){
      alert("ke trigger")
    },  
    PostItem : function() {
      alert("Ke Save Bro")
      try {
        axios
        .post("http://localhost:3000/admin/persyaratan", this.form)
        .then((response) => {
          this.form = [...this.form,response.persyaratan]
          this.form.id_persyaratan = "";
          this.form.id_jenis_persyaratan = "";
          this.form.nama_persyaratan = "";
          this.form.deskripsi_persyaratan = "";
          this.form.stuatus_persyaratan = "";
        })  
      } catch (error) {
        console.log(error);
      }
    },

    Edit(id) {
      this.updateSubmit = true;
      this.form.id = persyaratan.id;
      this.form.namaPersyaratan = persyaratan.namaPersyaratan;
      this.form.tipeData = persyaratan.tipeData;


    },

    Update(id) {
      axios
        .patch(`http://localhost:3000/persyaratan/${id}`, {
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

    Delete(id_persyaratan) {
      axios
        .delete("http://localhost:3000/admin/persyaratan/" + id_persyaratan)
        .then(() => {
          this.getItem();
          this.persyaratan.id_jenis_persyaratan="";
          this.persyaratan.nama_persyaratan = "";
          this.persyaratan.deskripsi_persyaratan = "";
          this.persyaratan.stuatus_persyaratan = "";
          alert("Deleted...");
        })
        .catch((err) => {
          console.log(err);
        });
    }
  },
  mounted() {
    this.getItem();
  },
};
</script>
  