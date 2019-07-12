# Oni configuration for Vim users

[Oni](github.com/onivim/oni) has several goals, one of them is `Ease the learning curve for new Vim users`.
That means that out of the box, Oni is geared towards beginners.
In this post I will supply configurations to remedy that and get a more traditional feel.

## TL;DR

The complete configs are at the bottom.

## How it works

Oni's configuration file is in practice a JavaScript file that it loads and runs on start.

The file can have any JS code, but it requires that its `export` part be a dictionary.
The keys are the name of the configs.
For example, the following is a config file that only sets the font size:

```js
module.exports = {
  "editor.fontSize": "14px",
}
```

You can also run code on start using the `activate` configuration:

```js
const activate = (oni) => {
  // Some complex confgs comes here
}

module.exports = {
  activate,
}
```

There is also the option to use a TypeScript (config.tsx) and thus gain auto-completion to the configuration file.
If a TypeScript config file is used, Oni generates a Javascript counterpart and uses it.
While this is neat, I currently don't use it as it requires platform-specific snippets.

## The complete configs

The recommended configs (can be copy-pasted):

```js
const activate = (oni) => {
  // Free-up default binding
  oni.input.unbind("<tab>")

  // Re-bind menu controls (like auto-completion)
  oni.input.bind("<enter>", "contextMenu.select")
  oni.input.bind("<tab>", "contextMenu.next")
  oni.input.bind("<S-Tab>", "contextMenu.previous")

  // Bind a show/hide control for the preview pane
  oni.input.bind("<f8>", "markdown.togglePreview")

  // Bind a show/hide control for the sidebar
  // (Relevant only if the sidebar is enabled below)
  oni.input.bind("<f9>", "sidebar.toggle")
};

module.exports = {
  activate, // A must for the above configs to be applied

  // Don't use since it is geared towards Vim newbies
  "oni.useDefaultConfig": false,

  // Do use my own Vim configs
  "oni.loadInitVim": true,

  // Minimalism
  "editor.maximizeScreenOnStart": true,
  "oni.hideMenu": true, // Can be opened using 'Alt' on non-Macs
  "sidebar.enabled": false, // Turn on if you prefer pretty GUI
  "tabs.height": "2.1em",

  // Pretty GUI
  "tabs.mode": "tabs",
  "sidebar.plugins.enabled": true,
  "experimental.markdownPreview.enabled": true,
}
```

# Subjective and "bleeding edge" configs

- [My actual Oni config](github.com/TalAmuyal/MyConfigs/blob/master/dotfiles/oni-config.js).
- [My (Neo)vim config](github.com/TalAmuyal/MyConfigs/blob/master/dotfiles/init.vim).

