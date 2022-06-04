<template>
  <div class="bg-dark h-screen">
    <div class="flex" style="height : 88vh">
      <!--SideNav-->
      <div class="w-56 bg-black h-full flex-none">
        <div class="p-6">  
          <img src="./assets/img/SpotifyLogoWhite.png" alt="Spotify Logo" class="h-10 " style="filter: brigthness(0) invert(1)">
        </div>
        <div class="mx-2 mb-5">
          <button v-for="page in pages" :key="page.id" 
            @click="setID = page.id"
            :class="`w-full focus:outline-none text-sm font-semibold rounded px-3 py-2 flex items-center justify-start ${setID === page.id ? 'bg-light text-white' : 'text-lightest'}`"
          >
            <i class="material-icons mr-3"> {{page.icon}} </i>
            <p> {{page.name}} </p>
          </button>
        </div>
        <div class="mx-5">
          <h1 class="text-xs mb-3 text-lightest tracking-widest uppercase">Playlists</h1>
          <button class="flex items-center justify-start opacity-75 hover:opacity-100 mb-2">
            <img src="./assets/img/addNew.png" alt="addNew" class="h-8 w-8 mr-3 ">
            <p class="text-sm text-white font-semibold">Create Playlist</p>
          </button>
          <button class="flex items-center justify-start opacity-75 hover:opacity-100">
            <img src="./assets/img/liked.png" alt="likedSongs" class="h-8 w-8 mr-3 ">
            <p class="text-sm text-white font-semibold">Liked Songs</p>
          </button>
          <div class="h-px w-full bg-light my-3">
          </div>
        </div>
        <div class="mx-5">
          <div class="w-full h-20 overflow-y-scroll">
            <p v-for="album in albums" :key="album.name" class="text-lightest hover:text-white text-sm py-1">
              {{album.name}}
            </p>
          </div>
          <button class="flex items-center justify-start text-lightest hover:text-white py-2 mt-4">
            <i class="material-icons mr-3 rounded-full border border-lightest text-sm">arrow_downward</i>
            <p class="text-sm font-semibold">Install App</p>
          </button>
        </div>
        <div class="relative">
          <div class="w-40 h-full flex justify-end items-start opacity-0 hover:opacity-100 p-2 absolute">
            <div class="bg-black rounded-full w-8 h-8 text-white">
              <i class="material-icons">keyboard_arrow_down</i>
            </div>
          </div>
          <img class="w-20 h-auto mx-auto" src="escuchado1.jpg" alt="playing">
        </div>
      </div>
      <!--MainContent-->
      <div class="w-full h-full relative overflow-y-scroll">
          <!--Header-->
          <div class="w-full sticky top-0 py-4 px-6 flex items-center justify-between bg-dark">
            <div class="flex items-center">
              <button class="rounded-full bg-black w-8 h-8 text-white mr-3">
                <i class="material-icons text-3xl">keyboard_arrow_left</i>
              </button>
              <button class="rounded-full bg-black w-8 h-8 text-white">
                <i class="material-icons text-3xl">keyboard_arrow_right</i>
              </button>
            </div>
            <div class="relative">
              <button @click="showDropdown = true" class="bg-light rounded-full py-1 px-2 flex items-center">
                <img src="./assets/img/myphoto.jpg" alt="myProfilePic" class="rounded-full h-6 w-6 mr-2">
                <p class="text-white font-semibold text-xs mr-3">Nicolas Meier</p>
                <i v-if="showDropdown === false" class="material-icons text-white">arrow_drop_down</i>
                <i v-else class="material-icons text-white">arrow_drop_up</i>
              </button>
              <div v-if="showDropdown === true" class="absolute bg-light w-full rounded mt-1">
                <button @click="showDropdown = false" class="focus:outline-none w-full text-sm py-2 text-lightest hover:text-white border-b border-white opacity-75 hover:opacity-100">Account</button>
                <button @click="showDropdown = false" class="focus:outline-none w-full text-sm py-2 text-lightest hover:text-white border-b border-light opacity-75 hover:opacity-100">Log Out</button>
              </div>
            </div>
          </div>
          <!--Cards-->
          <div class="px-6 py-3">
            <div class="flex items-center justify-between">
              <h1 class="pl-2 text-white text-2xl font-semibold tracking-wider hover:underline">Recently Played</h1>
              <h2 class="pr-8 pt-4 text-xs text-lightest uppercase tracking-wider hover:underline mb-3">See All</h2>
            </div> 
            <div class="w-full flex flex-wrap">
              <div v-for="recent in recents" :key="recent.title" class="p-2 w-48 relative">
                <div class="absolute w-full h-full flex items-end justify-end p-8 opacity-0 hover:opacity-100">
                  <div class="bg-green rounded-full h-10 w-10 flex items-center justify-center">
                    <i class="material-icons text-white text-2xl">play_arrow</i>
                  </div>
                </div>
                <div class="bg-light w-full h-auto p-5 rounded-lg shadow-md">
                  <img :src="recent.src" class="h-auto w-full shadow mb-2">
                  <h1 class="text-sm font-semibold text-white tracking-wide"> {{recent.title}} </h1>
                  <h2 class="text-xs text-lightest tracking-wide pb-5"> {{recent.artist}} </h2>
                </div>
              </div>
            </div>
          </div>
          <div class="px-6 py-3">
            <div class="pl-2">
              <h1 class="text-white text-2xl font-semibold tracking-wider hover:underline">Made For Nicolas</h1>
              <h2 class="text-sm text-lightest ">Get better recomendations the more you listen.</h2>
            </div> 
            <div class="w-full flex flex-wrap">
              <div v-for="custom in customs" :key="custom.title" class="p-2 w-48 relative">
                <div class="absolute w-full h-full flex items-end justify-end p-8 opacity-0 hover:opacity-100">
                  <div class="bg-green rounded-full h-10 w-10 flex items-center justify-center">
                    <i class="material-icons text-white text-2xl">play_arrow</i>
                  </div>
                </div>
                <div class="bg-light w-full h-auto p-5 rounded-lg shadow-md">
                  <img :src="custom.src" class="h-auto w-full shadow mb-2">
                  <h1 class="text-sm font-semibold text-white tracking-wide"> {{custom.title}} </h1>
                  <h2 class="text-xs text-lightest tracking-wide pb-5"> {{custom.artist}} </h2>
                </div>
              </div>
            </div>
          </div>
      </div>
    </div>
    <!-- PlayBar -->
    <div class="w-full flex items-center justify-between px-3 bg-light border-t border-dark" style="height: 12vh">
      <div class="flex items-center w-1/4">
        <div>
          <h1 class="text-sm text-white tracking-wide">Hace Casi 2000 años</h1>
          <h2 class="text-xs text-lightest tracking-wide">Ricardo Iorio</h2>
        </div>
        <i class="material-icons text-xl text-green mx-4">favorite</i>
        <i class="material-icons text-xl text-lightest hover:text-white">picture_in_picture_alt</i>
      </div>

      <div class="flex flex-col justify-center w-2/4 items-center">
        <div class="flex items-center">
          <button class="mx-5 text-lightest hover:text-white"><i class="material-icons text-lg">shuffle</i></button><!--1:12:54-->
          <button class="text-lightest hover:text-white"><i class="material-icons text-lg">skip_previous</i></button>
          <button class="rounded-full h-8 w-8 flex items-center justify-center mx-5 border-lightest border text-lightest hover:text-white"><i v-if="pause === false" @click.prevent="playSong(song), pause = true" class="material-icons">play_arrow</i><i v-if="pause === true" @click.prevent="pauseSong(), pause=false" class="material-icons">pause</i></button>
          <button class="text-lightest hover:text-white"><i class="material-icons text-lg">skip_next</i></button>
          <button class="mx-5 text-lightest hover:text-white"><i class="material-icons text-lg">repeat</i></button>
        </div>
        <div class="w-3/4 flex items-center mt-3">
          <p class="text-xs text-lightest mr-1">1:15</p>
          <div class="w-full h-1 bg-dark rounded-full flex items-center">
            <div class="h-1 rounded-full bg-green" style="width: 30%;">
            </div>
            <div class="h-3 w-3 bg-white rounded-full -ml-1 shadow">
            </div>
          </div>
          <p class="text-xs text-lightest ml-1">3:43</p>
        </div>
      </div>

      <div class="flex items-center w-1/4 justify-end">
        <i class="material-icons text-lightest hover:text-white">playlist_play</i>
        <i class="material-icons text-xl text-lightest hover:text-white mx-3">important_devices</i>
        <i class="material-icons text-xl text-lightest hover:text-white">volume_up</i>
        <div class="w-20 ml-1 bg-lightest rounded-full h-1"> 
        </div>
      </div>
    </div>
  </div>
</template>

<script>


export default {
  name: 'App',
  data() {
    return {
      pages : [
        {id: 'home', name: 'Home', icon: 'home'},
        {id: 'search', name: 'Search', icon: 'search'},
        {id: 'library', name: 'Your Library', icon: 'bar_chart'}
      ],
      setID: 'home',
      albums: [
        {name: 'Honestidad brutal'},
        {name: 'Cargar la suerte'},
        {name: 'Tuy'},
        {name: 'Chuy'},
        {name: 'Lolita'},
        {name: 'Carmesi'},
      ],
      showDropdown: false,
      recents: [
        {src: 'escuchado1.jpg', title: 'Avivando la Llama', artist: 'Ricardo Iorio'},
        {src: 'releaseradar.jpg', title: 'Release Radar', artist: 'By Spotify'},
        {src: 'descubrimiento.jpg', title: 'Discover Weekly', artist: 'By Spotify'},
        {src: 'tango-rock.jpg', title: 'Tango Rock', artist: 'Various'},
        {src: 'infaltables.jpg', title: 'Infaltables', artist: 'Various'}
      ],
      customs:[
        {src: 'asadito.jpg' , title: 'Asadito', artist: 'BySpotify'},
        {src: 'dailymix.jpg' , title: 'Daily Mix', artist: 'BySpotify'},
        {src: 'iconos.jpg' , title: 'Iconos del Rock', artist: 'BySpotify'},
        {src: 'metal.jpg' , title: 'Metal del Nuestro', artist: 'BySpotify'},
        {src: 'rocknacional.jpg' , title: 'Rock Nacional', artist: 'BySpotify'},
      ],
      pause : false,
      audio: new Audio('cancion.mp3'),
    }
  },
  methods: {
    playSong(){
      this.audio.play();
    }
    ,
    pauseSong(){
      this.audio.pause();
    }
  }
}
</script>

<style>

</style>
