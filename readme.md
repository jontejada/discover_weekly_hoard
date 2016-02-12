#discover_weekly_hoard
* visualize & save the Spotify "Discover Weekly" playlist

##"Discover Weekly" playlist
* Spotify recommended tracks based on own listening history & "what others are playlisting and listening to around the songs you love"
* auto-updated every monday morning
* exactly(?) 30 tracks, ~2 hrs
* no auto-archiving, refreshed playlist destroys previous <-- pain point
* [announcement](https://press.spotify.com/li/2015/07/20/introducing-discover-weekly-your-ultimate-personalised-playlist/)
* [verge article](http://www.theverge.com/2015/9/30/9416579/spotify-discover-weekly-online-music-curation-interview)
* [quartz article](http://qz.com/571007/the-magic-that-makes-spotifys-discover-weekly-playlists-so-damn-good/)

##tools & features
* [Spotify API](https://developer.spotify.com/web-api/)
	* [OAuth 2.0 authorization](http://oauth.net/) necessary to get user's playlists
	* get 'Discover Weekly' playlist
	* get track info, album art, etc
	* modify / create new playlists
	* [Spotify URIs and IDs](https://developer.spotify.com/web-api/user-guide/#spotify-uris-and-ids)
	* [Web API Object Model](https://developer.spotify.com/web-api/object-model/#external-id-object)
* [Echo Nest API](http://developer.echonest.com/docs/v4)
	* rich artist and song metadata
		* [acoustic attributes](http://developer.echonest.com/acoustic-attributes.html)
	* [Echo Nest was acquired by Spotify in 2014](https://developer.spotify.com/news-stories/2014/03/06/echo-nest-joins-spotify/)
	* [can use Spotify IDs](https://developer.spotify.com/spotify-echo-nest-api/)
	* [code examples](https://developer.spotify.com/web-api/code-examples/)
* app will live at http://www.jontejada.com/discover
	* [heroku hosting](https://www.heroku.com)
		* scheduling for weekly archiving
	* [express](http://expressjs.com/en/4x/api.html) framework
		* [express cheatsheet](http://ricostacruz.com/cheatsheets/express.html)
	* [ejs](https://www.npmjs.com/package/ejs) templates

##extra features to build
* nodemailer email sending with html, links, etc.
* knex for postgresql

##UX
* homepage with app info & user login button
	* authentication using [Authorization Code Flow](https://developer.spotify.com/web-api/authorization-guide/#authorization_code_flow)
* [Get a List of Current User's Playlists](https://developer.spotify.com/web-api/console/get-current-user-playlists/) with `GET https://api.spotify.com/v1/me/playlists`
	* search the returned data for "Discover Weekly" value from key "name" in the data.items array of playlist objects
	* (might need to edit the default offset/limit of this GET to find)
	* save the value of the corresponding "id" key
	* (necessary?) also save the href string and extract user id for later requests
* [Get a Playlist's Tracks](https://developer.spotify.com/web-api/get-playlists-tracks/) with `GET https://api.spotify.com/v1/users/{user_id}/playlists/{playlist_id}/tracks`
	* where `{user_id}` is "spotifydiscover"
	* where `{playlist_id}` is from the previous GET
	* save `data.items`, which is an array of track objects
* iterate through the track objects in this saved array for relevant info:
	* `trackObj.track.artists` is an array of artist objects
		* `trackObj.track.artists[0].name` is a string of the first artist name
	* `trackObj.track.album.images` is an array of three image objects 
		* dimensions are [0] 640x640px, [1] 300x300px, [2] 64x64px
		* `trackObj.track.album.images[1].url` is a string of the 300px image url
	* `trackObj.track.id` is the Spotify ID
* EJS to fill served html with 5x6 grid of 30 300px images



