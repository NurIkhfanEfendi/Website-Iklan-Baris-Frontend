<template>
  <div>
    <div class="container mt-3">
      <div class="row">
        <div class="col-lg-12 grid-margin stretch-card">
          <div class="card">
            <div class="card-body">
              <p class="text-center">Website Iklan Baris</p>
              <hr>
              <p class="card-description float-right">
                <b-button variant="success" v-b-modal.modalIklan v-on:click="Add">Pasang Iklan di sini</b-button>
              </p>
              <div class="table-responsive">
                <b-table striped hover :items="iklan" :fields="fields">
                  <template v-slot:cell(Aksi)="data">
                    <b-button size="sm" variant="info" v-on:click="Edit(data.item)" v-b-modal.modalIklan><i class="mdi mdi-pencil btn-icon-prepend"></i> Ubah</b-button>&nbsp;
                    <b-button size="sm" variant="danger" v-on:click="Drop(data.item.id)"><i class="mdi mdi-delete btn-icon-prepend"></i> Hapus</b-button>
                  </template>
                </b-table>
                <b-pagination
                  v-model="currentPage"
                  :per-page="perPage"
                  :total-rows="rows"
                  align="center"
                  v-on:input="pagination">
                </b-pagination>

                <b-toast id="loadingToast" title="Processing Data" no-auto-hide>
                  <b-spinner label="Spinning" variant="success"></b-spinner>
                  <strong class="text-success">Loading...</strong>
                </b-toast>

                <!-- toast untuk tampilan message box -->
                <b-toast id="message" title="Message">
                  <strong class="text-success">{{ message }}</strong>
                </b-toast>

              </div>
            </div>
          </div>
        </div>
      </div>
    </div>

    <b-modal 
      id="modalIklan"
      @ok="Save"
    >
      <template v-slot:modal-title>
        Form Pasang Iklan
      </template>
        <form ref="form">
            <div class="form-group input-group">
                <input class="form-control" placeholder="Judul Barang" type="text" v-model="judul">
            </div>
            <div class="form-group input-group">
                <input class="form-control" placeholder="Deskripsi Barang" type="text" v-model="deskripsi">
            </div>
            <div class="form-group input-group">
                <input class="form-control" placeholder="Harga Barang" type="text" v-model="harga">
            </div>
            <div class="form-group input-group">
                <input class="form-control" placeholder="Upload Foto Barang" type="text" v-model="foto">
             </div>
        </form>
    </b-modal>

  </div>
</template>


<script>
module.exports = {
  data : function(){
    return {
      search: "",
      id: "",
      judul: "",
      deskripsi: "",
      harga: "",
      foto:"",
      action: "",
      message: "",
      currentPage: 1,
      rows: 0,
      perPage: 10,
      key: "",
      iklan: [],
      fields: ["foto", "judul", "deskripsi", "harga", "Aksi"],
    }
  },

  methods: {
    getData : function(){
      let conf = { headers: { "Authorization" : 'Bearer ' + this.key } };
      let offset = (this.currentPage - 1) * this.perPage;
      this.$bvToast.show("loadingToast");
      this.axios.get("/iklan/" + this.perPage + "/" + offset, conf)
      .then(response => {
        if(response.data.status == 1){
          this.$bvToast.hide("loadingToast");
          this.iklan = response.data.iklan;
          this.rows = response.data.count;
        } else {
          this.$bvToast.hide("loadingToast");
          this.message = "Gagal menampilkan data iklan."
          this.$bvToast.show("message");
          // this.$router.push({name: "login"})
        }
        
      })
      .catch(error => {
        console.log(error);
      });
    },

    pagination : function(){
      if(this.search == ""){
        this.getData();
      } else {
        this.searching();
      }
    },

    Add : function(){
      this.action = "insert";
      this.judul = "";
      this.deskripsi = "";
      this.harga = ""; 
      this.foto = "";
    },

    Edit : function(item){
      this.action = "update";
      this.id = item.id;
      this.judul = item.judul;
      this.deskripsi = item.deskripsi;
      this.harga = item.harga;
      this.foto = item.foto;
    },

    Save : function(){
      let conf = { headers: { "Authorization" : 'Bearer ' + this.key } };
      this.$bvToast.show("loadingToast");
      if(this.action === "insert"){
        let form = new FormData();
        form.append("id", this.id);
        form.append("judul", this.judul);
        form.append("deskripsi", this.deskripsi);
        form.append("harga", this.harga);
        form.append("foto", this.foto);

        this.axios.post("/iklan", form, conf)
        .then(response => {
          this.$bvToast.hide("loadingToast");
          if(this.search == ""){
            this.getData();
          } else {
            this.searching();
          }
          this.message = response.data.message;
          this.$bvToast.show("message");
        })
        .catch(error => {
          console.log(error);
        });
      } else {
        let form = {
          judul: this.judul,
          deskripsi: this.deskripsi,
          harga: this.harga,
          foto: this.foto
        }
        this.axios.put("/iklan/" + this.id, form, conf)
        .then(response => {
          this.$bvToast.hide("loadingToast");
          if(this.search == ""){
            this.getData();
          } else {
            this.searching();
          }
          this.message = response.data.message;
          this.$bvToast.show("message");
        })
        .catch(error => {
          console.log(error);
        });
      }
    },

    Drop : function(id){
      let conf = { headers: { "Authorization" : "Bearer " + this.key} };
      if(confirm('Apakah anda yakin ingin menghapus data ini?')){
        this.$bvToast.show("loadingToast");
        this.axios.delete("/iklan/" + id, conf)
        .then(response => {
            this.getData();
            this.$bvToast.hide("loadingToast");
            this.message = response.data.message;
            this.$bvToast.show("message");
        })
        .catch(error => {
          console.log(error);
        });
      }
    },
  },
  mounted(){
    this.key = localStorage.getItem("Authorization");
    this.getData();
  }
}
</script>