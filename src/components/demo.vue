<template>
    <div>
        <header>
		<h1>Photo finder</h1>
	</header>
	
	<div id="app-instasearch">
	
		<div class="input-container">
			<input type="text" placeholder="Type a name" v-model="authorNameSearchString" />
		</div>
		
		<transition-group tag="ul" name="list-animation">
			
			<li class="photo photo-animated" v-for="photo in filteredPhotoFeed" v-bind:key="photo.id">
				<img v-bind:src="photo.download_url" />
				<span class="author">{{ photo.author }}</span>
			</li>
			
		</transition-group>
	
	</div>
    </div>
</template>

<script>
import axios from 'axios'
export default {
    data() {
        return {
        authorNameSearchString: "",
        photoFeed: null,
        searchString: null
        }
    },
    mounted() {
		axios
			.get('https://picsum.photos/v2/list?page=2&limit=10')
			.then(response => {
				this.photoFeed = response.data;
			})
    },
    computed: {
        
        filteredPhotoFeed: function () {
			
            var photos = this.photoFeed;
            var authorNameSearchString = this.authorNameSearchString;

            if(!authorNameSearchString){
                return photos;
            }

            // let searchString = authorNameSearchString.trim().toLowerCase();

            photos = photos.filter(function(item){
                if(item.author.toLowerCase().indexOf(authorNameSearchString) !== -1){
                    return item;
                }
            })

            return photos;
        }
	}
    
}
</script>

<style scoped>
* {
	margin: 0;
	padding: 0;
}

input:focus,
select:focus,
textarea:focus,
button:focus {
    outline: none;
}

html {
    overflow-y:scroll;
}

body {
	display: grid;
    grid-template-rows: 150px 1fr;
    background-color: #f5f5f5;
	font-family: 'Roboto Slab', serif;
	margin-bottom: 10px;
}

header {
	display: grid;
	color: white;
	background: #6D25BC;
}

header h1 {
	place-self: center;
	font-size: 42px;
}

#app-instasearch {
	place-self: center;	
	margin-top: 30px;
	width: 600px;
}

.input-container {
	border-radius: 5px;
	background: #677482;
	padding: 10px;
}

.input-container input {
	border: none;
	background: transparent;
	color: white;
	padding: 6px 15px;
	font-size: 18px;
}

::placeholder { /* Chrome, Firefox, Opera, Safari 10.1+ */
  color: #a6b0ba;
  opacity: 1; /* Firefox */
}

.photo {
	list-style: none;
	display: grid;
	grid-template-columns: 200px auto;
	margin-top: 20px;
	align-items: center;
	background-color: #e9edf0;
	padding: 30px 50px;
	border-radius: 5px;
	border: 1px solid #e3e3e3;
}

.author {
	font-size: 25px;
	margin-left: 20px;
	color: #75818e;
}

.photo img {
	border-radius: 5px;
	width: 200px;
}

.photo-animated {
	transition: all 0.5s;
}

.list-animation-enter, .list-animation-leave-to {
	opacity: 0;
	transform: translateY(30px);
}

.list-animation-leave-active {
	position: absolute;
}

</style>