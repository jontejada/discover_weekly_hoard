#discover_weekly_explorer

##uses the Spotify "Discover Weekly" playlist
* [announcement](https://press.spotify.com/li/2015/07/20/introducing-discover-weekly-your-ultimate-personalised-playlist/)
	* auto-updated every monday morning
	* exactly(?) 30 tracks
	* ~2 hrs
	* no auto-archiving, refreshed playlist destroys previous <-- pain point
* [verge article](http://www.theverge.com/2015/9/30/9416579/spotify-discover-weekly-online-music-curation-interview)
* [quartz article](http://qz.com/571007/the-magic-that-makes-spotifys-discover-weekly-playlists-so-damn-good/)

##tools & features
* [Spotify API](https://developer.spotify.com/web-api/)
	* [OAuth 2.0 authorization](http://oauth.net/) necessary to get user's playlists
	* get 'Discover Weekly' playlist
	* get track info, album art, etc
	* modify / create new playlists
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

##notes

my id : 124092907

spotify:user:spotifydiscover:playlist:6LA0z4WWp79Ggne8BxyuDo

https://api.spotify.com/v1/users/spotifydiscover/playlists/6LA0z4WWp79Ggne8BxyuDo

##workflow
* user login page
	* authentication using ['Authorization Code Flow'](https://developer.spotify.com/web-api/authorization-guide/#authorization_code_flow)
* [Get a List of a User’s Playlists
](https://developer.spotify.com/web-api/get-list-users-playlists/) with `GET https://api.spotify.com/v1/users/{user_id}/playlists`
	* search the returned data for "Discover Weekly" value from key "name" in the data.items array of playlist objects
	* might need to edit the default offset/limit of this GET to find
	* save the value of the corresponding "id" key
* [Get a Playlist's Tracks](https://developer.spotify.com/web-api/get-playlists-tracks/) with `GET https://api.spotify.com/v1/users/{user_id}/playlists/{playlist_id}/tracks`
	* 








