# Using a RichEmbed in a Command

You may have noticed that if you try to use a RichEmbed in your command, that there's no way to create the new embed, as `new Discord.RichEmbed()` is going to say `Discord` is undefined. That's because when using a RichEmbed, we need to require Discord.js alongside Commando.

```js
const commando = require('discord.js-commando');
const Discord = require('discord.js');
```

Now that it has been required, our RichEmbed won't be undefined. Let's create a new command that embeds the content of the user's message.

```js
const commando = require('discord.js-commando');
const Discord = require('discord.js');

module.exports = class EmbedCommand extends commando.Command {
    constructor(Client) {
        super(Client, {
            name: 'embed',
            group: 'group2',
            memberName: 'embed',
            description: 'Embeds the text you provide.',
            examples: [';embed Embeds are cool.'],
            args: [{
                key: 'text',
                prompt: 'What text would you like the bot to embed?',
                type: 'string'
            }]
        });    
    }

    run(message, args) {
        const text = args.text;
        const embed = new Discord.RichEmbed()
            .setDescription(text)
            .setAuthor(message.author.username, message.author.displayAvatarURL)
            .setColor(0x00AE86)
            .setTimestamp();
        return message.embed(embed);
    }
};
```

Simple isn't it? It's just like regular Discord.js RichEmbeds.

