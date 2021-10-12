---
type: posts
title: Automating your 'best of' playlist
date: 2021-10-11
categories: python
tags: automation
description: Automatically create spotify playlists from your top played songs
permalink: /automation/spotify-top-songs/
---

Spotify gives you a yearly playlist of your top songs for that year. But I've found myself wanting a playlist of my all time top played songs. A best of, so to speak.
Luckily the Spotify API gives us access to this information, and we can make a simple python program to automate it!

First off, we're going to be using [Spotipy][spotipy] to handle the interaction with the Spotify API. Spotipy has great instructions in it's
[Getting Started][spotipy-start] section, but in in brief you need to:
1. Go to the [Spotify developer dashboard][developer] and create a new app. Set the 'Redirect URI' to 'http://localhost:8080/callback/'
2. Save the client ID and client secret to environment variables in your shell's rc file:
```
export SPOTIPY_CLIENT_ID='your-spotify-client-id'
export SPOTIPY_CLIENT_SECRET='your-spotify-client-secret'
```
3. Install spotipy:
```
pip install spotipy
```

Open a new terminal to ensure the new environment variables are present. Now you're ready to run the `top_songs.py` script in the gist below:

{% gist f8ed7f824e502033f7a7004522f2d992 %}

The script is pretty easy to use, here's the CLI usage:

```
usage: top_songs.py [-h] [--term TERM] [--limit LIMIT] [--playlist PLAYLIST] [--existing URI] USER

Automates creation of a 'Top Songs' Spotify playlist

positional arguments:
  USER                  Spotify username

optional arguments:
  -h, --help            show this help message and exit
  --term TERM, -t TERM  Length of time to get top tracks over. Can be: short, medium, or long. Default: medium
  --limit LIMIT, -l LIMIT
                        Number of top tracks to add. Default: 50
  --playlist PLAYLIST, -p PLAYLIST
                        Top songs playlist name to create.Default: Top Songs
  --existing URI, -e URI
                        URI of top songs playlist if exists
```

* 'term' is the amount of time you want to get the top songs over. Spotify allows three time periods: short, medium, or long
* 'limit' is the number of tracks to get for the playlist. The maximum is 50
* 'playlist' is the name of the playlist to be created
* 'existing' is used when running this tool again to update an existing playlist. The first run will give you the new playlists URI,
and you can save this to use in the 'existing' argument later

The first time you use the script, a webpage for OAuth authentication with Spotify will open. Accept the app's scope, and the script will automatically run.
Any window it opens after can be closed. Spotipy will cache your credentials, so you only have to do this once. 

Here's some examples of running the script:

* To create a playlist for the first time:
```
$ python top_songs.py -t short $SPOTIFY_USERNAME
Created Top Songs playlist with URI: spotify:playlist:ABC123XYZ, please save this.
```

* To update a previously created playlist:
```
$ python top_songs.py -t short $SPOTIFY_USERNAME -e "spotify:playlist:ABC123XYZ"
```


[spotipy]: https://spotipy.readthedocs.io/en/2.19.0/#
[spotipy-start]: https://spotipy.readthedocs.io/en/2.19.0/#getting-started
[developer]: https://developer.spotify.com/dashboard/applications
