# Lecteur vidéo HLS avec Vue3-CLI [Fr]

https://github.com/video-dev/hls.js

## Mettre en place le projet
```
yarn install
```

### Démarrer un serveur de développement
```
yarn serve
```

### Compiler et minifier pour la production
```
yarn build
```

### installer Hls
```js
npm i hls.js
```

### importer Hls
```js
import Hls from 'hls.js';
```

### Quelques lignes importantes ( cf /src/views/Home.vue )

```js
 if (Hls.isSupported()) {...}
```
```js
let hls = new Hls();
hls.attachMedia(player);
```

```js
 hls.on(Hls.Events.MEDIA_ATTACHED, function () {
    console.log('player and hls.js sont liés !');
 });
```
```js
hls.loadSource('ma/source/video.m3u8');
```

```js
hls.on(Hls.Events.MANIFEST_PARSED, function (event, data) {
  console.log(
    'manifest loaded, found ' + data.levels.length + ' quality level'
  ); 
}
```
