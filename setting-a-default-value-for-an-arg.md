# Default

Sometimes you may want an argument to be optional. In that case, you can use `default`.

Let's say you have a command that rolls a dice, it's args would probably looking something like this:

```js
args: [
    {
        key: 'value',
        prompt: 'What is the maximum number you wish to appear?',
        type: 'integer'
    }
]
```

Let's say you wanted it to default to `6` if not set, like a real dice.

```js
args: [
    {
        key: 'value',
        prompt: 'What is the maximum number you wish to appear?',
        type: 'integer',
        default: 6
    }
]
```

And then it will be 6 if no argument is set.

You can take advantage of this to create completely optional arguments, for example:

```js
args: [
    {
        key: 'value',
        prompt: 'What is the maximum number you wish to appear?',
        type: 'integer',
        default: ''
    }
]
```

This sets the default to `''`, which is falsey. Then, in your run, you can handle that.

```js
const { value } = args;
if (!value) {
// do this
} else {
// do something else
}
```



