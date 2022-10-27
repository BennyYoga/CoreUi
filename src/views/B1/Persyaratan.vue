<template>
  <CRow>
    <CCol :xs="12">
      <CCard class="mb-4">
        <CCardHeader>
          <strong>Persyaratan</strong>
        </CCardHeader>
        <CCardBody>
            <CForm>
              <div class="mb-3">
                <CFormLabel for="exampleFormControlInput1">Nama Persyaratan</CFormLabel>
                <CFormInput type="text" placeholder="" aria-label="Nama Persyaratan"/>
              </div>
              <div class="mb-3">
                <CFormLabel for="exampleFormControlTextarea1">Tipe Data</CFormLabel>
                <CFormTextarea id="exampleFormControlTextarea1" rows="3"></CFormTextarea>
              </div>
              <div class="mb-3">
                <CFormLabel for="exampleFormControlInput1">Lenght</CFormLabel>
                <CFormInput type="text" placeholder="" aria-label="Lenght"/>
              </div>
              <div class="mb-3">
                <CButton color="info">Simpan</CButton>
              </div>
            </CForm>
        </CCardBody>
      </CCard>
    </CCol>
    
  </CRow>
</template>

<script>
export default {
  name: 'FormControl',
}
</script>
