 {% include styles.html %}

 {% include github-corner.html url="https://github.com/andrey-hilux/github-hls-video-player/" %}

# GitHub HLS Video Player

##### Maintenance Status: Stable

### The easiest way to host Your video on GitHub Pages directly

To ensure performance and reliability for their users, GitHub recommends repositories remain small, ideally less than 1 GB, and less than 5 GB is strongly recommended. Files that you add to a repository via a browser are limited to 25 MB per file. You can add larger files, up to 100 MB each, via the [command line](https://docs.github.com/en/articles/adding-a-file-to-a-repository-using-the-command-line). 

Being that our Video Player uses small (MP4) files or fragments, we still have the repository limit per 1 GB or 5 GB for each. **The GitHub HLS Video Player** uses **[HTTP Live Streaming (HLS)](https://github.com/videojs/http-streaming/blob/main/docs/README.md)** protocol in the sequence of small HTTP-based file downloads, each downloading one short chunk of an overall potentially unbounded transport stream.  

Unfortunately, all the major desktop browsers except for Safari are missing HLS support. This player is included [videojs-http-streaming](https://github.com/videojs/http-streaming) addresses that situation by providing a polyfill for HLS on browsers that have support for Media Source Extensions..

<sup id="git-hub-hls-video-player-tutorial-video"></sup>

{% include tutorial.html url="JTdCJTIyY29uZiUyMiUzQSUyMmh0dHBzJTNBJTJGJTJGYW5kcmV5LWhpbHV4LmdpdGh1Yi5pbyUyRmdpdGh1Yi1obHMtdmlkZW8tcGxheWVyJTJGdmlkZW8lMkZobHMlMkZ0dXRvcmlhbCUyRmNvbmYuanNvbiUyMiU3RA==" %}

<p class="no-html"><a href="https://andrey-hilux.github.io/github-hls-video-player/#git-hub-hls-video-player-tutorial-video"><img src="/video/hls/tutorial/poster.png" alt="github-hls-video-player"></a></p>

#### How to use

**1.** Create a [new GitHub repository](https://kbroman.org/github_tutorial/pages/init.html)
**2.**  Create `<your-local-repo-directory>` , a and Split your video (mp4) file toward m3u8  by [ffmpeg|download](https://www.ffmpeg.org/download.html):

```
mkdir "<your-local-repo-directory>\video\hls\<file-name-directory>"
"<path-to-ffmpeg-directory>\bin\ffmpeg.exe" -i "<source-file-full-path>.mp4" -b:v 300k -g 60 -hls_time 20 -hls_list_size 0 -force_key_frames expr:gte(t,n_forced*5) "<your-local-repo-directory>\video\hls\<file-name-directory>\v.m3u8"
```

[-force_key_frames expr | doc](https://www.ffmpeg.org/ffmpeg-all.html#toc-Advanced-Video-options)
**3.** Make the `poster.png` for your video and save  in to `<your-local-repo-directory>\video\hls\<file-name-directory>` directory
**4.** Create `conf.json` in `video/hls/<file-name-directory>` directory

```json
    {
    "t": "<title>",
    "p": "https://<your git name>.github.io/<your-repo-directory>/video/hls/<file-name-directory>/poster.png", // poster
    "subtitles": {
        "kind": "subtitles",
        "label": "Український",
        "srclang": "uk",
        "src": "https://<your git name>.github.io/<your-repo-directory>/video/hls/<file-name-directory>/subtitles/sub.ua.vtt"
    },
    "m3u8": "https://<your git name>.github.io/<your-repo-directory>/video/hls/<file-name-directory>/v.m3u8"
    }
```

*min config:*

```json
    {
    "t": "<title>",
    "p": "https://<your git name>.github.io/<your-repo-directory>/video/hls/<file-name-directory>/poster.png", // poster
    "m3u8": "https://<your git name>.github.io/<your-repo-directory>/video/hls/<file-name-directory>/v.m3u8"
    }
```

**5.** Generate video `url` address:

```js
btoa(encodeURIComponent(
    JSON.stringify({
        "conf": "https://<your git name>.github.io/<your-repo-directory>/video/hls/<file-name-directory>/conf.json",
    })))
```

**6.** Add `_includes` directory in to `<your-local-repo-directory>`

**7.** Add `<file-name-directory>.html` file in to `<your-local-repo-directory>/_includes` with:

```html
<style type="text/css">
    .git-hub--player iframe {
        height: 37em;
        width: 100%;
    }
</style>

<div class="git-hub--player" style="width: 100%;height: 100%;display: inline-flex;justify-content: center;flex-direction: column;align-items: center;">
    <iframe src="https://andrey-hilux.github.io/pub/apps/video-js/iframe.html#{{ include.url }}" style="position: relative;padding: 7vh 0; " scrolling="no" allowfullscreen="" frameborder="0">
    </iframe>
</div>
```

**8.** Insert video in your root `README.mb` :

![<your-repo-directory>](images\include_block.jpg)

**9.** Add references to page:

```
[![<your-repo-directory>](<your-repo-directory>/video/hls/<file-name-directory>/poster.png)](https://<your git name>.github.io/<your-repo-directory>/)
```

or

```

### [SEE THIS PAGE WITH VIDEO:](https://<your git name>.github.io/<your-repo-directory>/)

```

**10.** Go to `<https://github.com/<your git name>/<your-repo-directory>/settings/pages>` to public your site, in `Source` section select: `Branch:main` , `/ (root)` and click on save button

**11.** Upload GitHub Page public video folder `data/video/hls/<file-name-directory>` directory
  

```
    cd /D "<your-local-repo-directory>"
    
    git init

    git config user.email "<your git email>"
    git config user.name "<your git name>"

    git config core.autocrlf true

    git checkout -b main

    git remote rm origin
    git remote add origin https://<your git name>:<your git password>@github.com/<your git name>/<your git repo>.git
    
    git add ./

    git commit -m "main ✨ HOW TO commit"
    git push origin main -u -f

    git commit --allow-empty -m "Trigger rebuild"
    
```

the `<your git password>` better change to [personal access tokens](https://docs.github.com/en/rest/overview/other-authentication-methods#via-oauth-and-personal-access-tokens)

#### You can automate this process by one click with 

##### [Visual Studio Code USEFUL PANEL](https://andrey-hilux.github.io/vscode.extension.usefulPanel/)

## Donations

#### To support this project, you can make a donation to its current maintainer:  

<table style="width: 100%; border-style: none; "><thead></thead><tbody style="width: 100%; display: block; "><tr style="width: 100%; display: inline-block; border: none; background-color: unset; "><td colspan="2" style="width: 100%; display: inline-block; border: none; " align="center"><a href=""><img src="donate/donate.btn.png" alt="patreon"></a></td></tr><tr style="width: 100%; display: block; border: none; background-color: unset; "><td style="width: 10%; display: inline-block; border: none; ">&nbsp; </td><td style="width: 40%; display: inline-block; border: none; " align="center"><a href="donate/bitcoin-address.txt"><img src="donate/3E9CjNizGmbPWmVc5ptTabK4xKGkxwk4LZ.png" alt="bitcoin"></a></td><td style="width: 40%; display: inline-block; border: none; " align="center"><a href="https://www.patreon.com/andreyHilux"><img src="donate/patreon.png" alt="patreon"></a></td><td style="width: 10%; display: inline-block; border: none; ">&nbsp; </td></tr></tbody></table>

## Release Notes

### 0.0.1 | 2021/06/22

* Added support for `jumpTo`.
* Added the ability to move plugin settings into custom files.

More information in the [changelog](docs/CHANGELOG.md "Changelog")
