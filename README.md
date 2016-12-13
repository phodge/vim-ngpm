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

Whenever a plugin is installed or updated, NGPM makes a list of the mappings/functions/commands provided by the plugin, and asks whether you want to add each one to your config (default is Yes, but if there is a plugin that defines a mapping you don't like, this is your chance to opt out). You also have the option of changing the mappings/commands to something that works better for you. If there is a conflict such as an updated plugin defining a mapping that's already defined by another mapping, then you will be prompted to choose which one you want. Note that if you were using `:ngpm update` or `:ngpm add`, NGPM tries not to write changes to the config file or indexes until you have resolved the conflicts. This is to minimise scenarios where you produce a config file with conflicts that must be resolved on startup.

**Problem** How do we get other instances of vim to pick up the new plugin automatically?

Detecting Plugin Features
---

This is the hard part. :-( 

(1) We need a way to determine staticly:

* function names
* command names
* mappings
* autocmds / augroups
* anything else?

This is going to be extremely difficult/impossible if everything is defined in a `plugin/foo.vim` file.

(2) For each of the above we also need to pull out the appropriate help text so that NGPM can tell the user what each thing is when they're saying Yes or No to include it. *Maybe* if the plugin has a good help file, we might be able to extract the text.

(3) We need a way to load only _some_ of the things. This will be extremely difficult/impossible if the plugin defines everything in a big `plugin/somescript.vim`

(4) For `:ngpm disable` we need a way to unload all the things provided by a plugin. This will not be easy to do.

(5) We need a way to reload plugins reliably. This is mostly solved by (4) above, but we also need to detect if there is some sort of `s:` script variable or `g:plugin_loaded` guard and reset it before reloading all the script files. This will be necessary for `:ngpm update`

NGPM Plugin Definition
---

Assuming the entire world jumps on board with NGPM, we could allow plugin authors to add a an `plugin.ngpm` file which declares all the mappings, functions, how to reload the plugin etc. This would make *Detecting Plugin Features* trivial. Things you'd need to declare in a `plugin.ngpm`:

* Other plugins that are mandatory dependencies, along with the minimum versions required and any features from those plugins that should be exposed by *this* plugin.
* Other plugins that are recommended, along with the minimum versions required and possibly a subset of the features provided by those plugins.
* mappings
* functions
* commands
* how to load your plugin (in case it needs to call `jobstart()` before the autocommands get registered?)
* how to completely unload your plugin, including removing global variables and guards
* Any files you want to expose to `runtimepath` since this *won't* be done by default. E.g. if you want someone to be able to use `:syn include syntax/foo.vim` to include your `syntax/foo.vim`.

Recommended Plugins is for when your plugin provides a substantially better user experience when another plugin is also present. The user is prompted to install recommended plugins, and if a subset of features is nominated by _your_ plugin then we try to ask the user about enabling just those features from the recommended plugins. Ultimately the user has the choice to opt-out of installing the recommended plugins completely and your plugin needs to cope with this.

Mandatory Plugins is when your plugin needs things provided by another plugin in order to work. The user will be prompted to install the other plugin as well, or else your plugin will be disabled. The user will also be forced to upgrade to a newer version of the dependency in case they have explicitly decided to sit on an old version. The user does ultimately have the option of telling your plugin "Here use this other plugin instead of that one you wanted". This is useful when the user wants to install and use their own fork of `tpope/fugitive`.

Overall Benefits
---

* Install and configure new plugins without editing your vimrc
* If you have a dotfiles repo to manage your plugin list, committing/pushing is automated for you
* Cherry-pick just the plugin features you want
* On startup Vim only needs to load the compiled index files, rather than load `plugin/*.vim` files from every plugin 
* Substantially fewer things in 'runtimepath'
* NGPM allows you to create a "plugin" that is really just a thoughtfully curated set of dependencies.
