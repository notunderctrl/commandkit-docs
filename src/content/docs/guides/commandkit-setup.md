---
title: CommandKit setup
---

This is a simple overview of how to set up CommandKit with all the available options. You'd usually set this up in your entry point file (e.g. `index.js`) where you have access to your Discord client object.

```js
// index.js
const { Client, GatewayIntentBits } = require('discord.js');
const { CommandKit } = require('commandkit');
const path = require('path');

const client = new Client({
    intents: [
        GatewayIntentBits.Guilds,
        GatewayIntentBits.GuildMessages,
        GatewayIntentBits.MessageContent,
    ],
});

new CommandKit({
    client,
    commandsPath: path.join(__dirname, 'commands'),
    eventsPath: path.join(__dirname, 'events'),
    validationsPath: path.join(__dirname, 'validations'),
    devGuildIds: ['DEV_SERVER_ID_1', 'DEV_SERVER_ID_2'],
    devUserIds: ['DEV_USER_ID_1', 'DEV_USER_ID_2'],
    skipBuiltInValidations: true,
});

client.login('YOUR_TOKEN_HERE');
```

### Client intents

:::note
Some Discord.js properties are only accessible using the correct intents.
:::

Intents limit the data your bot receives from the Discord API. In the example above, the most important intents are already set (Guilds, Guild Messages, and Message Content). If you need access to more data such as Guild Members, you can add this into the `intents` array within the `Client`
constructor, a [list of intents can be found here](https://discord-api-types.dev/api/discord-api-types-v10/enum/GatewayIntentBits).

### Required properties

-   `client` - Your Discord.js client object.

### Optional properties

-   `commandsPath` - Path to the commands folder.
-   `eventsPath` - Path to your events folder.
-   `validationsPath` - Path to the validations folder. This will only work if `commandsPath` was provided.
-   `devGuildIds` - Array of development server IDs. Used to register and run developer only commands in specific servers.
-   `devUserIds` - Array of developer user IDs. Used to ensure developer only commands can only be ran by these users.
-   `skipBuiltInValidations` - A property that disables CommandKit's built-in validations.

:::note
It's highly recommended to use the "path" library to define your paths to avoid any file import issues.
:::
