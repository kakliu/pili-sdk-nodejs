# Pili server-side library for NodeJS

## Installaion

```
npm install pili --save
```

## Usage

### Configuration

```javascript
var Pili = require('pili');

var HUB = 'HUB_NAME';

var clientOptions = {
  accessKey: 'YOUR_ACCESS_KEY',
  secretKey: 'YOUR_SECRET_KEY'
};

// Replace with your customized domains
var publishOptions = {
  rtmpPublishHost:       'xxx.pub.z1.pili.qiniup.com',
  streamPublishKey:      'STREAM_PUBLISH_KEY',
  streamPublishSecurity: 'SECURITY' // 'static' or 'dynamic'
};

// Replace with your customized domains
var playOptions = {
  rtmpPlayHost: 'xxx.live1.z1.pili.qiniucdn.com',
  hlsPlayHost:  'xxx.hls1.z1.pili.qiniucdn.com'
};
```

### Client

#### Create a Pili client

```javascript
var client = new Pili.Client(clientOptions);
```

#### Create a new streamPublishKey

```javascript
var title = null;           // optional.
var hub = HUB;              // required.
var publishKey = null;      // optional.
var publishSecurity = null; // optional. 'static' or 'dynamic', 'dynamic' as default.

client.createStream(title, bub, publishKey, publishSecurity, function(err, data) {
  // handle request
});
```

#### Get a stream

```javascript
var streamId = null;
// Suppose you own a streamId.
client.getStream(streamId, function(err, data) {
  // handle request
});
```

#### Update a stream

```javascript
client.updateStream(streamId, publishKey, publishSecurity, function(err, data) {
  // handle request
});
```

#### List streams

```javascript
 var hub = HUB;     // required.
 var marker = null; // optional.
 var limit = 0;     // optional.
client.listStreams(hub, marker, limit, function(err, data) {
  // handle request
});
```

#### Delete a stream

```javascript
client.deleteStream(streamId, function(err, data) {
  // handle request
});
```

#### Get stream segments

```javascript
var startTime = 0;  // optional.
var endTime = 0;    // optional.
client.getStreamSegments(streamId, startTime, endTime, function(err, data) {
  // handle request
});
```

### Policy

#### Create a publish policy

```javascript
var publish = new Pili.PublishPolicy(publishOptions);

// Publish policy operations
var pushUrl = publish.url();
```

#### Create a play policy

```javascript
var play = new Pili.PlayPolicy(playOptions);

// Play policy operations
var preset = null;  // optional, just like '720p', '480p', '360p', '240p'. All presets should be defined first.

var rtmpLiveUrl = play.rtmpLiveUrl(preset);
var hlsLiveUrl = play.hlsLiveUrl(preset);
var hlsPlaybackUrl = play.hlsPlaybackUrl(preset);
```

## History

- 1.0.0
	- Init sdk
	- Add Stream API
	- Add publish and play policy