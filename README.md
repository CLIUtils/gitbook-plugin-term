# Term plugin for GitBook

This is the term plugin, based on the innovative [terminal](https://github.com/davidmogar/gitbook-plugin-terminal) plugin by David Mogar. However, it is much cleaner and more intuitive to use, and works on all backends.

## How can I use this plugin?

Add the following to your gitbook:

```json
"plugins" : [ "term" ],
```

This will set up everything for you. If you want some more control over the behaviour or the style of your term, just add this section too:

```json
"pluginsConfig": {
  "term": {
    "copyButtons": false,
    "fade": false,
    "style": "classic",
  }
}
```

The following are valid options for either for a block in block mode or the config file:

| Option        | Default        | Description                          |
| ------------- | -------------- | ------------------------------------ |
| `fade`        | `true`         | Fade non-input parts on hover        |
| `copyButtons` | `true`         | Add the copy button                  |
| `style`       | `"default"`    | Pick the style (based on term)   |
| `prompt`      | regexp (below) | The string to search for and replace in block mode |
| `linestyles`  | `true`         | Add per line styles (warning and error)    |


## Block based auto-colorization

The block based system using the GitBook block system and the keyword `term`. A named-group regular expression picks up the parts of your command line, and can be modified either in your defaults or per-block. This works in all backends, including the GitBook readme (json backend). When using this method, one copy button will be created that copies all commands.

The [regular expression](https://github.com/slevithan/xregexp/blob/master/README.md#usage-examples) that is used by default is:

```
"(?<prompt>[^\\$^#^:]*)(?<pathsep>:?)(?<path>[^\\$^#]*?)(?<delimiter>[\\$#] )(?<command>.*)$"
```

The only requirement is that a named group "`command`" exist if you use copyButtons. The others are iterated in order and added as `t-name` spans. This default looks form something like `prompt:path$ command` (or `#`).
You use it like this:

```
{% term lineStyles=true %}
foo@joe:~ $ ./myscript
Normal output line. Nothing special here...
But...
You can add some colors. What about a warning message?
[warning][WARNING] The color depends on the theme. Could look normal too
What about an error message?
[error][ERROR] This is not the error you are looking for
```


## Language based method

You can also use a language based method, where you use triple-backticks followed by `term` as the language. This will work inside another block, but will not handle non-default color styles well, nor can you change the defaults.

## Styles

Term has 6 styles:

* **default**: Looks just like normal GitBook. Until you hover.
* **black**: Just that good old black term everybody loves.
* **classic**: Looking for green color font over a black background? This is for you.
* **flat**: Oh, flat colors. I love flat colors. Everything looks modern with them.
* **ubuntu**: Admit it or not, but Ubuntu have a good looking term.
* **white**: Make your term to blend in with your GitBook.

