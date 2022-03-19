<template>
  <div class="divCen">
    <h3>{{ msg }}</h3>
    <h4>Student Scores Edit</h4>
    <p class="p-right">
      <router-link to="/" active-class="active">Back to home</router-link>
    </p>
    <table>
      <tr>
        <th>Id</th>
        <td>
          <input type="text" :value="id" readonly />
        </td>
      </tr>
      <tr>
        <th>Name</th>
        <input type="text" v-model="name" />
      </tr>
      <tr>
        <th>Gender</th>
        <input type="text" v-model="gender" />
      </tr>
      <tr>
        <th>Chinese</th>
        <input type="text" v-model="chinese" />
      </tr>
      <tr>
        <th>Math</th>
        <input type="text" v-model="math" />
      </tr>
      <tr>
        <th>English</th>
        <input type="text" v-model="english" />
      </tr>
    </table>
    <p>
      <button @click="btn_edit_stuinfo">Edit to Save</button>
    </p>
  </div>
</template>

<script>
export default {
  name: "StudentEdit",
  data() {
    return {
      msg: "Welcome to Student Management App",
      id: "",
      name: "",
      gender: "",
      chinese: "",
      math: "",
      english: "",
    };
  },
  created: function () {
    this.id = this.$route.params.id;
    let stuinfo = JSON.parse(localStorage.getItem("stu" + this.id));
    this.name = stuinfo.name;
    this.gender = stuinfo.gender;
    this.chinese = stuinfo.chinese;
    this.math = stuinfo.math;
    this.english = stuinfo.english;
  },
  methods: {
    
    btn_edit_stuinfo: function () {
      if (parseInt(this.id) <10000 || parseInt(this.id) >99999){
        alert("ID的长度必须为5");
        return;
        } 
      if (parseInt(this.chinese) < 0 || parseInt(this.chinese) > 100  ){
        alert("成绩必须在0-100");
        return;
        }
      if (parseInt(this.math)< 0 || parseInt(this.math) > 100  ){
        alert("成绩必须在0-100");
        return;
        }   
      if (parseInt(this.english) < 0|| parseInt(this.english) > 100  ){
        alert("成绩必须在0-100");
        return;
        }      
      let oStu = {
        id: this.id,
        name: this.name,
        gender: this.gender,
        chinese: this.chinese,
        math: this.math,
        english: this.english,
      };
      var key = "stu" + oStu.id;
      var stu = JSON.stringify(oStu);
      localStorage.setItem(key, stu);
      this.$router.push({ path: "/info" });
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3,
h4 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
input {
  width: 128px;
}
p {
  font-style: normal;
}
p.p-right {
  font-style: italic;
  text-align: right;
}
div.divCen {
  margin: 2px auto;
  width: auto;
}
table {
  width: 60%;
  margin: auto;
  border-collapse: collapse;
  border: 0;
  text-align: center;
}
th {
  background-color: #93daff;
  color: #000000;
}
th,
td {
  font-size: 0.95em;
  text-align: center;
  padding: 4px;
  border-collapse: collapse;
}
th,
td {
  border: 1px solid #c1e9fe;
  border-width: 1px 0 1px 0;
}
tr {
  border: 1px solid #c1e9fe;
}
tr:nth-child(odd) {
  background-color: #dbf2fe;
}
tr:nth-child(even) {
  background-color: #fdfdfd;
}
</style>
