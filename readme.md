#discover_weekly_explorer

##uses the Spotify "Discover Weekly" playlist
* [announcement](https://press.spotify.com/li/2015/07/20/introducing-discover-weekly-your-ultimate-personalised-playlist/)
	* updated every monday morning
	* 30 tracks, about 2 hrs
	* no archiving!
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
	* [Echo Nest was acquired by Spotify in 2014](https://developer.spotify.com/news-stories/2014/03/06/echo-nest-joins-spotify/)
	* [can use Spotify IDs](https://developer.spotify.com/spotify-echo-nest-api/)
* app will live at http://www.jontejada.com/discover
	* [heroku hosted](https://www.heroku.com)
		* scheduling for weekly archiving
	* express
	* ejs



##extra features to build
* nodemailer email sending with html, links, etc.
* knex for postgresql