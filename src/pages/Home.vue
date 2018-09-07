<template>
  <f7-page>
    <f7-navbar sliding>
      <f7-nav-left>
        <f7-link icon-f7="icon-bars" panel-open="left"></f7-link>
      </f7-nav-left>
      <f7-nav-title>
        Home
      </f7-nav-title>
    </f7-navbar>
    <f7-block-title>{{ title }}</f7-block-title>
    <f7-block inner>
     <f7-card class="demo-card-header-pic" v-for="lecture in lectures">
  <f7-card-header
    
    class="no-border"
    valign="bottom"
    style="background-image:url(http://www.weather1.com/assets/images/wallpapers/fly00711_sm.jpg)"
  >{{lecture.data().name}}</f7-card-header>
  <f7-card-content>
    <p class="date">Posted on January 21, 2015</p>
    <p>Quisque eget vestibulum nulla. Quisque quis dui quis ex ultricies efficitur vitae non felis. Phasellus quis nibh hendrerit...</p>
  </f7-card-content>
  <f7-card-footer>
    <f7-link>Like</f7-link>
    <f7-link href="/about/">Read more</f7-link>
  </f7-card-footer>
</f7-card>
    </f7-block>

  </f7-page>
</template>
<script>
import firebase from 'firebase'
export default {
  name: 'Home',
  data() {
    return {
      title: 'Hello World',
      lectures:[],
      pageSize:10,
       email:'',
      password:''
    };
  },
  methods:{
    getLectures(){
      let query = firebase.firestore().collection('lectures').orderBy("name","desc")
      query.get()
    .then(docs=>{
      docs.forEach(doc=>{
        this.lectures.push(doc);
        console.log(doc)
      })
    
    }).catch(err=>{
      console.log(err)
    })
    },
      enter(){
     
      firebase.auth().createUserWithEmailAndPassword(this.email,this.password).then((data)=>{
console.log('the data is ',data)
      }).catch(err=>{
        console.log(err)
      })
    }

  },
  created(){
    this.getLectures()
  }
};
</script>

