WebSocket allows two-way, event-driven communication between web browser and server.

video tutorial: [How to use WebSockets - JavaScript Tutorial For Beginners](https://youtu.be/FduLSXEHLng)

index.js server side code - WebSocket server running on port 8082.
```js
let WebSocket = require("ws");

const wss = new WebSocket.Server({
  port: 8082,
});

wss.on("connection", (ws) => {
  console.log("New Client Connected!");

  ws.on("message", (data) => {
    console.log(`client has sent us: ${data}`);
    ws.send(data.toString().toUpperCase());
  });
  ws.on("close", () => {
    console.log("Client has disconnected!");
  });
});
```

index.html client side code.
```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>WebSocket Basics</title>
  </head>
  <body>
    <script>
      const ws = new WebSocket("ws://localhost:8082");
      ws.addEventListener("open", () => {
        console.log("We are connected.");
        ws.send("Hey How is it going?");
      });

      ws.addEventListener("message", ({ data }) => {
        console.log(data);
      });
    </script>
  </body>
</html>
```