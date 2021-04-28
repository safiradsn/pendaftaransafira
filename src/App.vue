<template>
  <div>
    <h1><center><b>FORM PENDAFTARAN ANGGOTA</b></center></h1>
    <form @submit.prevent="add">
      <input type="hidden" v-model="form.id">
      Nama:<br>
      <input type="text" v-model="form.name">
      <br><br>
      Jenis Kelamin: <br>
      <input type="text" v-model="form.jenis_kelamin">
      <br><br>
      Agama: <br>
      <input type="text" v-model="form.Agama">
      <br><br>
      Tanggal Lahir: <br>
      <input type="text" v-model="form.Tanggal_Lahir">
      <br><br>
      Telepon: <br> 
      <input type="text" v-model="form.Telepon">
      <br><br>
      Email:<br>
      <input type="text" v-model="form.Email">
      <br><br>
      Alamat: <br>
      <input type="text" v-model="form.Alamat">
      <br><br>
      <button type="submit" v-show="!updateSubmit">add</button>
      <button type="button" v-show="updateSubmit" @click="update(form)">Update</button>
    </form>
    <title>Table</title>
    <center><table border="1" id="customers">
        <tr>
          <th width="150px">Nama</th>
          <th width="150px">Jenis kelamin </th>
          <th width="150px">Agama</th>
          <th width="150px">Tanggal lahir</th>
          <th width="150px">Telepon</th>
          <th width="150px">Email</th>
          <th width="150px">Alamat</th>
          <th width="150px">Action</th>
        </tr>
    <tr v-for="user in users" :key="user.id">
        <td>{{user.name}}</td> &#160;
         <td>{{user.jenis_kelamin}}</td> &#160;
          <td>{{user.Agama}}</td> &#160;
           <td>{{user.Tanggal_Lahir}}</td> &#160;
            <td>{{user.Telepon}}</td> &#160;
             <td>{{user.Email}}</td> &#160;
              <td>{{user.Alamat}}</td> &#160;
        <button id="button" class="material-icons" @click="auto_edit(user)">edit</button> || <button id="button1" class="material-icons" @click="auto_delete(user)">delete</button>
    </tr>
    </table>
    </center>
    </div>
</template>

<script>
/* eslint-disable */
import axios from 'axios'
export default {
  data(){
    return{
      form: {
        id: '',
        name: '',
        jenis_kelamin: '',
        Agama: '',
        Tanggal_Lahir: '',
        Telepon: '',
        Email: '',
        Alamat: '',
        Action: ''
      },
      users: '',
      updateSubmit: false
      }
    },
  mounted() {
    this.load()
  },
  methods: {
    load(){
      axios.get('http://localhost:3000/users').then(res => {
        this.users = res.data
      }).catch ((err) => {
        console.log(err);
      })
    },
    add(){
      axios.post('http://localhost:3000/users/', this.form).then(res => {
        this.load()
        this.form.name = ''
        this.form.jenis_kelamin = ''
        this.form.Agama = ''
        this.form.Tanggal_Lahir = ''
        this.form.Telepon = ''
        this.form.Email = ''
        this.form.Alamat = ''
      })
    },
    edit(user){
    this.updateSubmit = true
    this.form.id = user.id
    this.form.name = user.name
    this.form.jenis_kelamin = user.jenis_kelamin
    this.form.Agama = user.Agama
    this.form.Tanggal_Lahir = user.Tanggal_Lahir
    this.form.Telepon = user.Telepon
    this.form.Email = user.Email
    this.form.Alamat = user.Alamat
  },
    update(form){
    return axios.put('http://localhost:3000/users/' + form.id , {name: this.form.name, jenis_kelamin: this.form.jenis_kelamin, Agama: this.form.Agama, Tanggal_Lahir: this.form.Tanggal_Lahir, Telepon: this.form.Telepon, Email: this.form.Email, Alamat: this.form.Alamat}).then
    (res => {
      this.load()
      this.form.id = ''
      this.form.name = ''
      this.form.jenis_kelamin = ''
      this.form.Agama = ''
      this.form.Tanggal_Lahir = ''
      this.form.Telepon = ''
      this.form.Email = ''
      this.form.Alamat = ''
      this.updateSubmit = false
    }).catch((err) => {
      console.log(err);
    })
  },
  del(user){
  axios.delete('http://localhost:3000/users/' + user.id).then(res =>{
    this.load()
    let index = this.users.indexOf(form.name)
    this.users.splice(index,1)
  })
}
}
}
</script>