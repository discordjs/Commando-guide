# Setting a Database Provider

Commando has a built-in way of storing guild settings. By default things such as the guild's custom prefix or disabled commands will be stored for Data Persistence, and you can also have your own custom settings as well.

Setting a Database Provider is simple, and there are many ways to accomplish it.

1. You can use an sqliteProvider, which comes built-in with Commando.
2. You can use the [SequelizeProvider](https://github.com/WeebDev/Commando/blob/master/providers/Sequelize.js), created by Crawl.
3. You can find another or make your own.

This chapter will only go over the first one.

sqliteProvider comes built-in with Commando, you won't have to copy any files to use it. It's actually extremely simple, all you need to do is, firstly, install sqlite.

`npm i -S sqlite`

Then, require it of course.

`const sqlite = require('sqlite');`

And lastly, setup the provider.

```js
client.setProvider(
	sqlite.open(path.join(__dirname, 'settings.sqlite3')).then(db => new Commando.SQLiteProvider(db))
).catch(console.error);
```

And there, an sqlite provider.

 

