
<template>
  
  <v-card>
  
    <v-layout>
      <v-navigation-drawer
        style="background-color: rgb(203, 203, 203); "
        expand-on-hover
        rail
      >  
        <v-list>
          <v-list-item class="back"
            prepend-icon="fa fa-user-circle" 
            title="Sohaib Ali"  
          ></v-list-item>
        </v-list>
      
         <v-divider></v-divider> 
        
        <v-list density="compact" nav >
          <v-list-item class="back" prepend-icon="fa-solid fa-house" title="Home" value="myfiles"> </v-list-item>
          <v-list-item class="back" prepend-icon="fa fa-address-book" title="About" value="shared"></v-list-item>
          <v-list-item class="back" prepend-icon="fa fa-user" title="Login" value="starred"></v-list-item>
        </v-list>
     
      </v-navigation-drawer>
       
      <v-main >
        <v-card class="slide">
     <div class="Onetypes">
    <div id="app" class="web-camera-container">
    <div class="camera-button">
    <button type="button" class="button is-rounded" :class="{ 'is-primary' : !isCameraOpen, 'is-danger' : isCameraOpen}" @click="toggleCamera">
      <span v-if="!isCameraOpen"><v-btn>Camera</v-btn></span>
      <span v-else>Close Camera</span>
  </button>
</div>
<div v-show="isCameraOpen && isLoading" class="camera-loading">
  <!-- <ul class="loader-circle">
    <li></li>
    <li></li>
    <li></li>
  </ul> -->
</div>
<div v-if="isCameraOpen" v-show="!isLoading" class="camera-box" :class="{ 'flash' : isShotPhoto }">
  
  <div class="camera-shutter" :class="{'flash' : isShotPhoto}"></div>
    
  <video v-show="!isPhotoTaken" ref="camera" :width="450" :height="337.5" autoplay></video>
  
  <canvas v-show="isPhotoTaken" id="photoTaken" ref="canvas" :width="450" :height="337.5"></canvas>
</div>

<div v-if="isCameraOpen && !isLoading" class="camera-shoot">
  <button type="button" class="button" @click="takePhoto">
    <img src="https://img.icons8.com/material-outlined/50/000000/camera--v2.png">
  </button>
</div>

<div v-if="isPhotoTaken && isCameraOpen" class="camera-download">
  <a id="downloadPhoto" download="my-photo.jpg" class="button" role="button" @click="downloadImage">
    Download
  </a>
</div>
</div>
     </div>
    <v-layout  >
      <nav class="navbar navbar-expand-lg  bg-dark">
  <a class="navbar-brand" href="#">LOGO HERE</a>
  <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
    <span class="navbar-toggler-icon"></span>
  </button>

  <div class="collapse navbar-collapse" id="navbarSupportedContent">
    <ul class="navbar-nav mr-auto">
    </ul>
    <form class="form-inline my-2 my-lg-0">
      <input class="form-control mr-sm-2" type="search" placeholder="Search" aria-label="Search">
      <button class="btn btn-outline my-2 my-sm-0" type="submit">Search</button>
    </form>
  </div>
</nav>
      
    </v-layout>
    <div class="container-fluid  " >
        <div class="row">
          <div class="col-lg-4 col-md-6">
          <div class="classone">
            <h4>Text Here</h4>
            <p class="para">Lorem, ipsum dolor sit amet consectetur adipisicing elit. Illum minus debitis laboriosam iure id eaque quibusdam obcaecati ipsum veniam, ut delectus, consequuntur in esse rem, eum eius commodi soluta. Sequi eum harum magni, possimus dolorem eligendi impedit, architecto nostrum accusantium amet voluptatem libero, cupiditate expedita ipsam atque quis! Labore consequuntur blanditiis voluptas eum debitis tempore impedit obcaecati dicta maiores non ex repellat, consequatur nobis.</p>
          </div>
          </div>
          <div class="col-lg-4 col-md-6">
            <div class="classone"><h4>Contact</h4>
             <p >Lorem, ipsum dolor sit amet consectetur adipisicing elit. Illum minus debitis laboriosam iure id eaque quibusdam obcaecati ipsum veniam, ut delectus, consequuntur in esse rem, eum eius commodi soluta. Sequi eum harum magni, possimus dolorem eligendi impedit, architecto nostrum accusantium amet voluptatem libero, cupiditate expedita ipsam atque quis! Labore consequuntur blanditiis voluptas eum debitis tempore impedit obcaecati dicta maiores non ex repellat, consequatur nobis.</p>
            </div>
          </div>
          <div class="col-lg-4 col-md-6">
            <div class="classone"><h4>Textarea</h4>
            <textarea name="" id="" cols="47" rows="10"></textarea><br>
           
            <button>Submit </button>
            </div>
          </div>
        </div>
      </div>
      
  </v-card>
 
      </v-main>
    </v-layout>
  </v-card>
</template>
<!-- script apply -->
<script>

export default {
  name: 'HelloWorld',
   data() {
    return {
      isCameraOpen: false,
      isPhotoTaken: false,
      isShotPhoto: false,
      isLoading: false,
      link: '#'
    }
  },
  
  methods: {
    toggleCamera() {
      if(this.isCameraOpen) {
        this.isCameraOpen = false;
        this.isPhotoTaken = false;
        this.isShotPhoto = false;
        this.stopCameraStream();
      } else {
        this.isCameraOpen = true;
        this.createCameraElement();
      }
    },
    
    createCameraElement() {
      this.isLoading = true;
      
      const constraints = (window.constraints = {
        audio: false,
        video: true
      });


      navigator.mediaDevices
        .getUserMedia(constraints)
        .then(stream => {
          this.isLoading = false;
          this.$refs.camera.srcObject = stream;
        })
    },
    
    stopCameraStream() {
      let tracks = this.$refs.camera.srcObject.getTracks();

      tracks.forEach(track => {
        track.stop();
      });
    },
    
    takePhoto() {
      if(!this.isPhotoTaken) {
        this.isShotPhoto = true;

        const FLASH_TIMEOUT = 50;

        setTimeout(() => {
          this.isShotPhoto = false;
        }, FLASH_TIMEOUT);
      }
      
      this.isPhotoTaken = !this.isPhotoTaken;
      
      const context = this.$refs.canvas.getContext('2d');
      context.drawImage(this.$refs.camera, 0, 0, 450, 337.5);
    },
    
    downloadImage() {
      const download = document.getElementById("downloadPhoto");
      const canvas = document.getElementById("photoTaken").toDataURL("image/jpeg")
    .replace("image/jpeg", "image/octet-stream");
      download.setAttribute("href", canvas);
    },
  }
}

</script>
<!-- script apply -->
<!-- css apply -->
<style scoped>
.container-fluid{
  margin-top: 40px;
}
textarea{
  background-color:white;
}
.Onetypes{
  background: #343A40;
}
.Onetypes button{
background: rgb(203, 203, 203);
color: black;
height: 50px;
margin: auto;
width: 100%;
}
.back{
  background-color:#343A40;
  color:white;
}
.Mainone{
  font-size: large;
  margin-left: 100px;
}
.form-inline{
  float: inline-end;
}
.navbar{
 
  width: 100%;
}
.navbar-brand{
  color:white;
}
.navbar-brand:hover{
  color:white;
}
.classone{
  background: rgb(203, 203, 203);

}
.classone{
  border: 3px solid gray;
  box-shadow: 8px 3px 15px gray;
  margin-top: 20px;
  padding: 15px;
  border-radius: 12px;
  border-bottom-left-radius: 50px;
  border-top-right-radius: 50px;
  width: 100%;
  height: 400px;
}
.classone h4{
  text-align: center;
}

.btn-outline{
color: white;
border-color: white;

}

.classone button{
  color: white;
  background:#343A40;
  width: 80px;
  height: 30px;
  border-radius: 10px;
}
</style>
<!-- css apply -->
