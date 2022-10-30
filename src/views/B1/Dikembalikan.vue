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
                  <CTableRow>
                    <CTableDataCell>user1</CTableDataCell>
                    <CTableDataCell>Lorem Ipsum</CTableDataCell>
                    <CTableDataCell>22/11/2002</CTableDataCell>
                    <CTableDataCell>Event</CTableDataCell>
                  </CTableRow>
                  <CTableRow>
                    <CTableDataCell>user2</CTableDataCell>
                    <CTableDataCell>Lorem Ipsum</CTableDataCell>
                    <CTableDataCell>22/11/2002</CTableDataCell>
                    <CTableDataCell>Event</CTableDataCell>
                  </CTableRow>
                </CTableBody>
              </CTable>
          </CCardBody>
        </CCard>
      </CCol>
    </CRow>
  </template>
  
  <script>
  export default {
    name: 'Tables',
  }
  </script>
  