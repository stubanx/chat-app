
---

## Project Folder Structure

The project folder should contain the following files:

- `package.json`
- `index.html`
- `app.js`
- `test/index.test.js`

## Running the Application

To see the layout of the app, run:

```bash
pear dev
```

**Note:** Close the app before installing dependencies. If dependencies are installed while the app is running, an error will be thrown.

## Modules Used

The app uses the following modules:

- `hyperswarm` to connect peers on a "topic".
- `hypercore-crypto` for basic cryptography.
- `b4a` to manipulate buffers.

## Installing Dependencies

Install the dependencies with:

```bash
npm install hyperswarm hypercore-crypto b4a
```

## Running Multiple Instances

Open two app instances by running `pear dev` in two terminals. For now, you will need to specify a different storage directory for the second Pear instance to allow for two instances to run simultaneously:

```bash
pear dev -s /tmp/tmp_pear_instance
```

## Using the Application

1. In the first app, click on **Create**. A random topic will appear at the top.
2. Note that topics consist of 64 hexadecimal characters (32 bytes).
3. Paste the topic into the second app, then click on **Join**.
4. Once connected, messages can be sent between each chat application.

## Discussion

### Chatting With Another Machine

The two application instances use Hyperswarm's distributed hash table (DHT) to connect with each other.

The DHT enables connections across different machines, so chatting with other people is also possible, as long as they run the same application.

One option is to copy the code, but it is also possible to distribute the application itself over the DHT. This is the topic of **Sharing a Pear Application**.

### Joining Topics VS Joining Servers

In a traditional client-server setup, the server is hosted at an IP address (or hostname) and a port, e.g., `http://localhost:3000`. This is what clients use to connect to the server.

The code in `app.js` contains the line:

```javascript
swarm.join(topicBuffer, { client: true, server: true });
```

`topicBuffer` is the invitation: anyone who knows this topic can join the room and message the other members.

Note that all members are equal: there is no separate client or server. If the room creator goes offline, or even deletes the room from their machine, the other members can continue chatting.

## Frontend Frameworks

Any frontend framework can be used with Pear.

---
