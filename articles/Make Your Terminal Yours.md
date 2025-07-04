# How I set up my terminal

The terminal is an engineer's Alpha and Omega. Where everything starts, runs and ends. So customizing it according to your preferences can bring noticeable differences to your workflows. Here's how I customize mine:

## ZSH and OH-MY-ZSH

If you're still using bash, you might be missing out. Zsh, or the Z shell, is an extended Bourne shell with a lot of improvements. The real magic, however, happens when you combine it with [Oh My Zsh](https://ohmyz.sh/). It's an open-source, community-driven framework for managing your Zsh configuration. It comes bundled with thousands of helpful functions, helpers, plugins, and themes that will make you say "wow". Installation is as simple as a single command from their website.

---

## Aliases for most used commands

Typing the same long commands is tedious and a waste of time. Aliases are essentially shortcuts for commands. You define a short, easy-to-remember alias for a longer command, and your shell will substitute it.

I have a bunch of them in my `.zshrc` file. Here are some of my git-related favorites:

```bash
alias g='git'
alias ga='git add'
alias gc='git commit -m'
alias gp='git push'
alias gl='git log --oneline --decorate --graph'
alias gs='git status'
```
With these, `git status` becomes a quick `gs`. It's a small change that adds up.

---

## A Good Font for a Good Vibe

To get the best out of modern themes and prompts (like those from Oh My Zsh), you'll want a font that can handle special characters and glyphs. Powerline fonts are perfect for this.

I'm a big fan of [Fira Code](https://github.com/tonsky/FiraCode) and [Cascadia Code](https://github.com/microsoft/cascadia-code) which also support programming ligatures. This means characters like `->` or `!=` are combined into a single, more readable symbol. You can find these and many others at [Nerd Fonts](https://www.nerdfonts.com/). Once you've installed a font, just select it in your terminal's preferences.

---

## Supercharge with Plugins

Plugins are what take Zsh from a good shell to an amazing one. Oh My Zsh makes managing plugins a breeze. Here are a few that I can't live without:

*   **`zsh-autosuggestions`**: This plugin suggests commands as you type, based on your history. You can complete the suggestion with the right arrow key. It's like your shell is reading your mind.
*   **`zsh-syntax-highlighting`**: This highlights commands in the terminal. It's great for catching syntax errors before you even run the command.
*   **`git`**: This one is enabled by default with Oh My Zsh and provides a ton of git aliases and helper functions.

To add plugins, just add their names to the `plugins=(...)` list in your `.zshrc` file.

---

## Manage Sessions with a Terminal Multiplexer

A terminal multiplexer like `tmux` is a powerful tool. It lets you create multiple "windows" and "panes" within a single terminal window. This is amazing for multitasking.

But the killer feature is session management. You can detach from a session, and all the processes in it will keep running in the background. You can then log off, go home, ssh back into your machine, and reattach to the session exactly where you left off. It's a lifesaver for remote work.

---

## Keep it all safe with Dotfiles

After setting up your terminal perfectly, you'll want to back up your configuration. All these settings are stored in configuration files in your home directory, often called "dotfiles" because their names start with a dot (e.g., `.zshrc`, `.tmux.conf`, `.gitconfig`).

A common practice is to store these dotfiles in a Git repository on GitHub. This way, you not only have a backup, but you can also easily sync your configuration across multiple computers. A little bit of setup here will save you a lot of time in the future.

---

And that's a wrap! Your terminal is a very personal space. These are just some of the ways I've made mine feel like home. Dive in, experiment, and make your terminal truly yours.