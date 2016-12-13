# vim-ngpm
Next-Gen Package Manager

Uses a human-readable config file to describe which plugins to load, and which features to use from them.

* config file layout / ordering is extremely deterministic - there is only one correct way to do each thing
* if user edits the file directly, don't allow saving unless it is formmated exactly right
* provide a shortcut to reformat the file if the user gets stuck
* also need good syntax errors I guess
* provide userland commands for making changes to the file (adding/deleting/modifying things)
* we could even do a 'git commit' for the user if we see that the file is in a "dotfiles" repo
* config file is compiled to some sort of index that can be loaded quickly by vim/neovim
* config file includes exact tags or commit refs for each plugin to guarantee stability

When you've chosen a plugin to load, you can choose to load any or all of its:

* globally-namespaced functions (autoload# namespaced functions are always available)
* mappings
* globally-namespaced commands (autoload# commands are always available)
* autocmds

You can also set default values for `g:whatever` variables here in a declarative form.

* A `g:something` variable needs to be associated with a plugin so that when you disable/delete a plugin you don't leave extra vars laying around.
* If two plugins want a `g:something` variable, it gets defined in both places but they must have exactly the same value.

If vim/neovim adds support, you may be able to add load these things from plugins in the future:

* replacements for built-in commands like `:s[ubstitute]` and `:make`
* replacements for built-in features like `/` or `=` or `hjkl` movement
* replacements for built-in functions like `bufname()`
* plugin-defined &options

And very importantly, if two or more plugins provide the same thing (e.g, a `<leader>x` mapping), you will be forced (prompted) to choose which of the plugin's mappings gets loaded. There would be some sort of syntax for this, such as:

    plugin 'user/what' {
      imap \x <mapping> suppress('otherplugin', otherotherplugin')
    }

The compiled index includes an exact version/commit reference for each plugin referenced, this way NGPM knows that whatever is in the index will always work.

User Experience
---

`:ngpm add <plugin>` Add a plugin to the config file, start downloading it in the background

`:ngpm disable <plugin>` Disable a plugin that's already in the config file. Remove all its mappings/functions/options etc. Turn on mappings/functions/commands from other plugins that were being suppressed by this plugin.

`:ngpm update [<pattern>]` Update one or more plugins in the background.

Whenever a plugin is installed or updated, NGPM makes a list of the mappings/functions/commands provided by the plugin, and asks whether you want to add each one to your config (default is Yes, but if there is a plugin that defines a mapping you don't like, this is your chance to opt out). If there is a conflict such as an updated plugin defining a mapping that's already defined by another mapping, then you will be prompted to choose which one you want. Note that if you were using `:ngpm update` or `:ngpm add`, NGPM tries not to write changes to the config file or indexes until you have resolved the conflicts. This is to minimise scenarios where you produce a config file with conflicts that must be resolved on startup.


