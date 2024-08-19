---
layout: post
title: "Why Pay for Streaming? Build Your Own Media Server at Home"
date: 2024-08-19
---

# Why Pay for Streaming? Build Your Own Media Server at Home

<aside>
⚠️ DISCLAIMER: Author of this article is not responsible for the actions of the reader.
Follow proper internet safety and check how strict is your country in enforcing their internet laws.

</aside>

## Why?

- ***Because if buying isn't owning, piracy isn't stealing.***
- You're a hoarder like me.

## Installation and configuration

Let's populate your library first.

There is the standard way of getting things. The usual, search for "xyz torrent"and download it manually. But we're gonna automate this as much as we can.

If you already have a bunch of stuff downloaded, then that is also fine.

1. [**Radarr**](https://radarr.video/): A movie collection manager.
2. [**Sonarr**](https://sonarr.tv/): A TV series collection manager.
3. [**Jackett**](https://github.com/Jackett/Jackett): A tool that provides access to multiple torrent trackers.
4. [**Flaresolverr**](https://github.com/FlareSolverr/FlareSolverr): A proxy server to bypass Cloudflare protection.
5. [**qBittorrent**](https://www.qbittorrent.org/): A torrent client. 

You can install Radarr and Sonarr as services. This way they can start themselves as services automatically on system startup.

<aside>
⚠️ Do not download other random torrent clients, like uTorrent; those are borderline malware.

</aside>

<aside>
💡 Always get the software from official sources.

</aside>

### qBittorrent

Do the usual setup.

- Configure your default download directory
- Configure download and upload speeds / limits.
- Configure a good (=>1.0) seeding ratio. [A good pirate always seeds]

Now the main setup:

- Setup Web UI remote control.
- Add the IP Address. [0.0.0.0 for using every network interface in your system]
- Setup username and password

Example settings:

![Example Settings](/media/media-server-image.png)

### Flaresolverr

Setting this up is as straight forward as it gets.

Just download and run. [You may need to run as administrator]

Note the port it is running on. Default should be 8191.

### Jackett

Jackett is an easy way to setup "Indexers". An indexer is basically a website (or API) which lets you search for the media you want to download.

Some famous indexers for example: YTS, 1337x, eztv, thepiratebay etc

- Default settings should be fine.
- Add the flaresolverr URL with port; eg: [http://localhost:8191](http://localhost:8191/)

**Lets add some indexers.**

There are 3 types of indexers:

- **Public**: Basically free and no account required. This is what you'll be using the most.
- **Semi-private:** Usually need an account. Usually the accounts are somewhat difficult to get (you have to be invited, or buy access etc)
- **Private**: Paid accounts. If you've got the money, this is the best option, obviously.

Setup some popular public indexers. 

- Click on add indexer.
- Filter by Type = Public
- Add an indexer
    - Depending on your internet provider and country, you will probably not have access to the official site of the indexer.
    - So, to add the indexer, you have to figure out the proper working link
    - Open the multiple URLs provided in the dialog.
    - Keep the one that is working for you.
    - For example, for YTS, this is the configuration I have to use.
    
    ![Add indexer dialogue](/media/media-server-image%201.png)
    

Click on "Test All" to test the indexers are working or not.

<aside>
💡 If the none of the site provided in the dialog are not working for you, you can try to figure out a working proxy yourselves. Also make sure that flaresolverr is running.

</aside>

### Radarr and Sonarr

Setting up Radarr and Sonarr is quite similar. So this section should cover both.

- Setup Folders
    - Goto Setting → Media Management
    - Add folder where your library will be
    - You can setup multiple folders accross drives
    
- Setup the "Download Client" as qbittorrent
    - Add the host, port, username and password
    - Add category as "radarr" and "sonarr" respectively
    - Click on "Test" button to test if the connection works.
        - If your connection does not work, check your settings on qbittorrent Web UI.

![Download clients settings](/media/media-server-image%202.png)

**Optional**:

If you check the "Remove Completed" option, Radarr will delete torrent entries and the files from your temporary download folder and move them to your library folder.

This is good (for most) but it will also make it so that seeding is stopped for the same torrent; which is not good.

![Download client settings dialogue](/media/media-server-image%203.png)

- Setup Indexers
    - Add a new indexer
    - Here, select "Torznab"
    - Goto Jackett UI and click on "Copy Torznab Feed"; Paste this in the URL section
    - Goto Jackett UI and copy the API Key at the top; Paste this in the API Key section
    - Click on Test to test the connection. Then Save.
    
    ![Add indexer dialogue](/media/media-server-image%204.png)
    

At this point, you *should* be able to search and add movies / series.

Simply, search for them on the Radarr / Sonarr UI and add them and it should start downloading.

---

## Optional (but still somewhat useful) configurations

### Size Limits:

One important thing to configure when setting up Radarr and Sonarr is the size limits and profiles.

Unless you want to download a 2k resolution movie that is like 50GB or something.

You can setup limits like this:

![Size limits in quality settings page](/media/media-server-image%205.png)

Example:

![Size limit warning in interactive search results](/media/media-server-image%206.png)

<aside>
💡 This will limit your choices when auto downloading some titles. When that happens you can choose to override the limit and download anyway.

</aside>

Quality profiles:

![Quality Profiles page](/media/media-server-image%207.png)


### Language Profiles (Sonarr)

This is kind of annoying, but if you want to download non-english TV series or any Anime, make sure to add a new Language profile in the profiles section.

Also make sure to select this Language profile when adding new series to Sonarr otherwise it will never find your show.

![I have selected every language option here](/media/media-server-image%2015.png)

Adding a french TV Series here as example:
![Adding a french TV Series here as example](/media/media-server-image%2016.png)


### Search filters:

You can setup filters and use them while using Interactive Search:

![Interactive search filter](/media/media-server-image%208.png)

### Telegram Bot:

Setup a notifier bot

![Telegram notifier bot](/media/media-server-image%209.png)

---

## Adding new media

Search:

![Movie search screen](/media/media-server-image%2010.png)

And add:

![Movie add dialogue](/media/media-server-image%2011.png)

When added:

![Movie page](/media/media-server-image%2012.png)

If you want to manually search for a media:

![Interactive search](/media/media-server-image%2013.png)

---

## How to watch

Now that we have a sizeable library, lets add some media players to keep easily visualize our library, watch our media and keep track of what we have watched.

We will use [Jellyfin](https://jellyfin.org/) for this.

Let's setup Jellyfin + Kodi.

If you have a digital TV, you can setup Kodi on it. For the rest of the devices we'll use Jellyfin.

Also, we'll use Jellyfin to manage watched history and the library and import that in Kodi.

### Jellyfin

Installation of Jellyfin should be simple.

Just download the installer and start the service.

Configuration:

- Dashboard → Libraries → Add Media Library → Your library folder(s).
- Dashboard → Users → ➕ → Add User: To create a new user
- Use this username and password on your remote devices to access your library.

<aside>
💡 To access your Jellyfin server remotely via different devices, you may need to configure firewall and port forward the proper ports on your host machine (and router)

</aside>

</br>

![Jellyfin homepage](/media/jellyfin.png)

### Transcoding Media

<aside>
💡 Please read this section carefully

</aside>

To watch media remotely, the media needs to be compatible with the device you are using. eg: Jellyfin on phone will refuse to play x265 encoded files

If the media is not compatible with your device, Jellyfin will try to transcode the file (using ffmpeg).

This increases CPU usage on the host device.

If you are using a Raspberry device to host your media servers, or if you are using the host for any other tasks like me (I use my gaming PC to host my media server), please ensure that your system can handle this load.

For example, if I try to stream 1080p x265 media on my phone, CPU usage on my PC will climb up +60-70%. So, if I'm playing games at the same time someone is using the media server, it would obviously make my game performance worse.

BUT

If you want to disable transcoding, you will have to disable it for a user.

Goto Dashboard → Users → Select the user you want to disable transcoding for and uncheck these options:

![Transcoding settings](/media/media-server-image%2014.png)

This will completely disable transcoding for that user. So, they cannot play unsupported formats directly from their Jellyfin app.

BUT

If the user is so inclined, they can directly download the media file via Jellyfin onto their device and watch it using a proper media player (example: VLC for android).

### Kodi

Download and install [Kodi](https://kodi.tv/).

This should be straight forward.

Don't need to configure any library sources on Kodi. We will do that using Jellyfin + Kodi.

![Kodi Movies page](/media/kodi.png)

### Jellyfin + Kodi

Follow instructions here: [https://jellyfin.org/docs/general/clients/kodi/](https://jellyfin.org/docs/general/clients/kodi/) and setup "Jellyfin for Kodi"

Now this will sync your Kodi library with Jellyfin library so that you can preserve what you were watching across devices (Just like netflix).

![thats-all-folks](/media/media-server-thats-all-folks.png)

There are a lot of tips and tricks I've probably missed out on. I've been torrenting stuff for years now and you pick up on stuff over time. Like understanding media quality and codecs from the title of torrents, picking up best sources etc.

Cant really put everything in one single article. Feel free to open issues for discussion.

---

# Other cool resources

You'll find better and more in-depth guides about these services elsewhere on the internet. I'll add some of them when I come across them.
But this is how I've done my setup and this guide can be used as a good basic config for everything.

I have Bazarr setup as well but I dont use it as much. Only use it to find subtitles when my any of the media dont have subs + Jellyfin + Kodi plugins for finding subtitles also fail.


I'll keep updating this doc whenever I get around to setup other things like Prowlarr, Jellyseer, Lidarr, etc. (Except Plex, it fucking sucks)


- [Trash Guides](https://trash-guides.info/)
- [Servarr Wiki](https://wiki.servarr.com/)
- [Reddit](https://www.reddit.com/r/Piracy/comments/pqsomd/the_complete_guide_to_building_your_personal_self/)
- [HomeServer Reddit](https://www.reddit.com/r/HomeServer/)
