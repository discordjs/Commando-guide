# Validators

Sometimes you're going to want an argument to be a certain thing, for example, a certain text, or maybe you want to check the length, there's many things you may want to do. This can be accomplished with a `validate` in your arg.

Let's say you have a command where your first argument has to match a certain text, for example if we wanted our say command to only allow 200 characters to be said, and no more. It's very simple.

First, let's pull our argument from our say command:

```js
args: [
    {
        key: 'text',
        prompt: 'What text would you like the bot to say?',
        type: 'string'
    }
]
```

Let's add a blank `validate` to the arg.

```js
args: [
    {
        key: 'text',
        prompt: 'What text would you like the bot to say?',
        type: 'string',
        validate: text => {}
    }
]
```

Inside our validate, let's check to see if the length is below 201 characters, and return `true` if it does.

```js
validate: text => {
    if (text.length < 201) return true;
}
```

Now, below that, let's let it return an error message if that check does not pass.

```js
validate: text => {
    if (text.length < 201) return true;
    return 'Message Content is above 200 characters';
}
```

In the end, your args should look like this:

```js
args: [
    {
        key: 'text',
        prompt: 'What text would you like the bot to say?',
        type: 'string',
        validate: text => {
            if (text.length < 201) return true;
            return 'Message Content is above 200 characters';
        }    
    }
]
```

And now you've got a validator.

