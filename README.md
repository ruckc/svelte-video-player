
# Svelte Video Player Kit

This is a convenience fork of the original package which had some issues with SSR and sveltekit at the time this publishing. 

[https://github.com/meigo/svelte-video-player
](https://github.com/meigo/svelte-video-player)

All other credits go to the original author of the package.

## Installation

```bash
pnpm install -D svelte-video-player-kit
# OR
npm install svelte-video-player-kit
```

## Basic video player component for svelte, sapper and legacy apps.

Controls are tabbable and respond to key presses (enter/space/arrows) where applicable.

Starting a player will pause previously playing video player instance.

Fullscreen functionality is disabled on iPhone, other than that should function fairly smoothly in both desktop and mobile browsers.

## Demo

https://svelte-video-player.netlify.app/

## Props

| Prop name       | Type                                | Default value          | Description                                                                                                 |
| :-------------- | :---------------------------------- | ---------------------- | ----------------------------------------------------------------------------------------------------------- |
| width           | <code>string &#124; number</code>   | <code>1920</code>      | Real width of video for calculating aspect ratio for responsive design                                      |
| height          | <code>string &#124; number</code>   | <code>1080</code>      | Real height of video for calculating aspect ratio for responsive design                                     |
| poster          | <code>string</code>                 | <code>''</code>        | Absolute or relative URL of poster image                                                                    |
| source          | <code>string &#124; string[]</code> | <code>''</code>        | Absolute or relative URL (or array of those) of video source. Supported formats are `webm`, `mp4` and `ogg` |
| controlsHeight  | <code>string</code>                 | <code>'55px'</code>    | Height of bottom control bar, rescaling included components                                                 |
| trackHeight     | <code>string</code>                 | <code>'6px'</code>     | Height of playbar and volume slider tracks                                                                  |
| thumbSize       | <code>string</code>                 | <code>'15px'</code>    | Size of playbar and volume slider thumb                                                                     |
| centerIconSize  | <code>string</code>                 | <code>'60px'</code>    | Size of center icon                                                                                         |
| playerBgColor   | <code>string</code>                 | <code>'black'</code>   | Color of player background                                                                                  |
| color           | <code>string</code>                 | <code>'#FF3E00'</code> | Main color of control components                                                                            |
| focusColor      | <code>string</code>                 | <code>'white'</code>   | Color of focus outlines                                                                                     |
| barsBgColor     | <code>string</code>                 | <code>'white'</code>   | Background color of playbar and volume slider tracks                                                        |
| iconColor       | <code>string</code>                 | <code>'white'</code>   | Color of button icons                                                                                       |
| bufferedColor   | <code>string</code>                 | <code>'#FF9600'</code> | Color of buffered chunks                                                                                    |
| borderRadius    | <code>string</code>                 | <code>'8px'</code>     | Rounded corner radius of the player.                                                                        |
| skipSeconds     | <code>string &#124; number</code>   | <code>5</code>         | Skipping time in seconds                                                                                    |
| chunkBars       | <code>boolean</code>                | <code>false</code>     | Display overlay with buffered and played parts of video                                                     |
| loop            | <code>boolean</code>                | <code>false</code>     | Play video in loop                                                                                          |
| controlsOnPause | <code>boolean</code>                | <code>true</code>      | Show control bar when video is paused                                                                       |
| timeDisplay     | <code>boolean</code>                | <code>false</code>     | Display current time beside playbar                                                                         |

## Usage

If aspect ratio of the video is other than default 16:9 provide `width` and `height` props to player for calculating aspect ratio to prevent [CLS](https://web.dev/cls/).
Real size of video player will be determined by it's parent element.

### Import directly to svelte or sapper apps

See [Example App.svelte](./example/src/App.svelte).

```html
<script>
  import VideoPlayer from 'svelte-video-player';

  const poster = 'https://www.server.com/poster.jpg';
  const source = [
    'https://www.server.com/video.webm',
    'https://www.server.com/video.mp4',
    'https://www.server.com/video.ogv',
  ];
</script>

<VideoPlayer {poster} {source} />;
```

```js
<VideoPlayer poster="poster_url" source="video_url" />
```

```js
<VideoPlayer width="500" height="500" poster="./local_poster.jpg" source="./local_video.mp4" loop />
```

### For legacy apps load prebuilt script and stylesheet from unpkg.com

Example: https://codepen.io/meigo-kukk/pen/yLVMZBO

```html
<html>
  <head>
    <link rel="stylesheet" href="https://unpkg.com/svelte-video-player@latest/dist/svelte-video-player.css" />
    <script src="https://unpkg.com/svelte-video-player@latest/dist/svelte-video-player.js"></script>

    <script>
      function initPlayer() {
        let player = new VideoPlayer({
          target: document.getElementById('player'),
          props: {
            poster:
              'https://res.cloudinary.com/animaly/image/upload/c_scale,w_960/v1608783923/ntiiorkrkxba6kmooa4u.gif',
            source:
              'https://res.cloudinary.com/animaly/video/upload/ac_aac,vc_h264/v1608783907/xixhbu5v9aawqqgiafri.mp4',
            controlsHeight: '55px',
            centerIconSize: '60px',
            color: 'deepskyblue',
          },
        });
      }
    </script>
  </head>
  <body onload="initPlayer()" style="background-color:#333">
    <div style="max-width: 600px; margin: 0 auto;">
      <div id="player" />
    </div>
  </body>
</html>
```
