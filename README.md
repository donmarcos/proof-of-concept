## Proof of Concept
Getting geo-location to work in Vue 

---

### References
+ https://www.npmjs.com/package/vue2-google-maps
+ https://alligator.io/vuejs/vue-google-maps/  
+ https://medium.com/netscape/deploying-a-vue-js-2-x-app-to-heroku-in-5-steps-tutorial-a69845ace489  
+ https://youtu.be/RbFNihP7H7I

---

### Create a vue project  
    + $ `vue create project_name`

---

### Change directories into your new project  
    + $ `cd project_name`

---

### $ `npm install vue2-google-maps --save`

---

### Get a key from Google Maps
    + https://console.developers.google.com/apis
    + On the left of the page, Click on Credentials - API Key (the key icon)
    + This will give you your API Key
    + It should look something like this: `AWzaSyC13JVX4Fa8C2mqaI42QhxqSIONruP0z9A`

---

### Update your `main.js` file to look like this:

#### main.js
```js
import Vue from 'vue'
import App from './App.vue'
import * as VueGoogleMaps from 'vue2-google-maps'

Vue.config.productionTip = false

Vue.use(VueGoogleMaps, {
  load: {
    key: 'USE YOUR OWN GOOGLE MAP API KEY', /* this numer is your key from Google you just got */
    libraries: 'places',
  }
})

new Vue({
  render: h => h(App)
}).$mount('#app')
```

---

###  Add this to your `App.vue` file

#### App.vue
```vue
<template>
  <div id="app">

    <div ref="vgmap">
    <gmap-map class="google-map"
      :center="center"
      :zoom="inzoom">
      <gmap-marker
        :key="index"
        v-for="(m, index) in markers"
        :position="m.position"
        :clickable="true"
        :draggable="false"
      ></gmap-marker>
    </gmap-map>
    </div>

  </div>
</template>

<script>

  export default {
    name: 'app',
    mounted: function() {
      this.geolocation()
    },
    data () {
      return {
        inzoom : 15,
        center: {lat: 10.0, lng: 10.0},
        markers: [],
/*        markersx: [
         {position: {lat: 10.0, lng: 10.0}},
         {position: {lat: 11.0, lng: 11.0}}
        ]*/
      }
    },
    methods: {
      geolocation() {

        navigator.geolocation.getCurrentPosition((position) => {
          this.center = {
            lat: position.coords.latitude,
            lng: position.coords.longitude,
          }
          var myPosition = {position: { lat: position.coords.latitude,
                              lng: position.coords.longitude,}};
          this.markers.push(myPosition);
          console.log(myPosition);
          console.log(this.markers);
        });

     }
    }
  }
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

  .google-map {
    width: 700px;
    height: 400px;
    margin: 0 auto;
    background: gray;
  }

  .button {
     display: inline-block;
     margin: -4px;
  }

</style>

```

---

### To view your project in your browser
$ `npm run serve`

---

### Next LoveLA meeting
+ June 9th

Some goals for Saturday 6/9/2018  meeting 

some ideas on how we can make the 
traveling route to work 
http://geekonjava.blogspot.com/2016/05/demo-animated-moving-marker-on-google.html

Rails back end 

1 - Create API Rest end point 
    GET to retrieve GPS points to draw markers on Gmap vue 
	json object should look like :
	{position: {lat: 10.0, lng: 10.0}}
	
2 - create on the db backend a table of gps points with lat and long entries 

3 - lets focus on one of the metro lines , maybe the red line ? 
     - do we have a pic of every station along the route ? 
     - do we have the gps locations of every station  ? 
     - we will need a table on our end to keep that info 
	 

Vue side 

2 - Implement Axio ( http resources on the current code )
    to use the rails backend API 
	
---
+ June 30th

