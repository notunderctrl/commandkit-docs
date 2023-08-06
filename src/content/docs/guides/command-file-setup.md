---
title: Commands Setup
---

CommandKit supports both slash commands and context menu commands. And since both have very similar triggers (interactions) and command structures, they are both stored and handled from within the commands directory for convenience.

This is a simple overview of how to set up a simple "ping" slash command that simply replies with "Pong!".

```js
// commands/misc/ping.js
module.exports = {
    data: {
        name: 'ping',
        description: 'Pong!',
    },

    run: ({ interaction, client }) => {
        interaction.reply(`:ping_pong: Pong! ${client.ws.ping}ms`);
    },

    options: {
        devOnly: true,
        guildOnly: true,
        userPermissions: ['Administrator', 'AddReactions'],
        botPermissions: ['Administrator', 'AddReactions'],
        deleted: false,
    },
};
```

### Required properties

Every command file must export an object with the following properties:

-   `data` - An object containing the command's structural information. This what will be used to register and handle your commands.

    This can also be set to the [`SlashCommandBuilder`](https://discord.js.org/docs/packages/builders/0.16.0/SlashCommandBuilder:Class) class, or the [`ContextMenuCommandBuilder`](https://discord.js.org/docs/packages/builders/0.16.0/ContextMenuCommandBuilder:Class) class if that's what you're comfortable with.

-   `run` - A function that will be called when your command is executed. This function also has an object passed to it as an argument with the following properties:
    -   `interaction` - The interaction object that triggered the command. This can either be a chat input interaction or a context menu interaction.
    -   `client` - The Discord client object.

### Optional properties

There is an additional optional property that can also be exported within the object above:

-   `options` - An object which tells the command how to behave during registration and handling. This object has the following optional properties:
    -   `devOnly` - A boolean that determines whether the command should only be registered in development guilds and by the bot developers. These properties are setup as `devGuildIds` and `devUserIds` when [instantiating `CommandKit`](/guides/commandkit-setup/).
    -   `guildOnly` - A boolean that determines whether the command should only be handled in guilds.
    -   `userPermissions` - An array of permission strings/bits that determines whether the user has the required permissions to execute the command. This is checked against the user's permissions in the guild where the command was executed (if any).
    -   `botPermissions` - An array of permission strings/bits that determines whether the bot has the required permissions to execute the command. This is checked against the bot's permissions in the guild where the command was executed (if any).
    -   `deleted` - A boolean that determines whether the command should be deleted on the next app restart.
