# [spectacle](https://github.com/FormidableLabs/spectacle)-sync

💁 Present Spectacle presentations synchronised on multiple devices.

- You create a new session and share the token with your audience
- Your viewers open the presentation and join the session
- All viewers' browsers will connect to yours via WebRTC
- Proceed to give the most stylish presentation imaginable 🕶

<img src="demo.gif" />

## Getting Started

If you haven't set up your presentation you can use `create-react-app` to get started:

```
create-react-app my-presentation --scripts-version spectacle-scripts
```

Once you have your presentation, just install `spectacle-sync` from npm:

```
yarn add spectacle-sync
```

To add it to your presentation, all you need to do is to wrap your `<Deck>` in another component:

```js
import React, { Component } from 'react';
import { Spectacle, Deck } from 'spectacle';
import NetworkSync from 'spectacle-sync';

export default class Presentation extends Component {
  render() {
    return (
      <NetworkManager>
        <Deck>
          // ...
        </Deck>
      </NetworkManager>
    );
  }
}
```

Then just start your app as usual and you will be greeted by the connection manager.
There you can either enter a token that you've been given and join an existing session,
or create a new one, which will generate a new token for you to share.

After you close the connection manager by clicking anywhere, you will find a small indicator
on the bottom left, informing you of the status of the WebRTC connection(s).

## How it works

When establishing a session a WebSocket connection is opened which by default connects to
`https://spectacle-signalling.now.sh`. This server takes care of registering sessions
and clients, and established the WebRTC peer to peer connections.

All of the viewers' browsers connect to the presenter's browser, which then proceeds to send
Spectacle's local storage changes over the connection. Nice!

The signalling server is in this same repo under `server/` and you can start your own
if you want.

## API

The only exposed API is the `NetworkSync` component which accepts the following props:

| Name | PropType | Description |
| ---- | -------- | ----------- |
| signalUri | PropTypes.string | Used to change the default signalling server |

