# ShellColorD

This repo includes a daemon that leverages shell escape codes to change a
running terminal colorscheme. It opens a socket that can be interacted with,
allowing you to remotely update colors of all your running shells. You can
easily deactivate the daemon on any given shell, allowing you to change colors
on all shells except ones that are running ssh, for example.

## Usage

Configure your color at `$XDG_CONFIG_DIR/shellcolor.conf`. Use `base00` through `base16`.

Add `shellcolord $$ &` (or `$fish_pid` on fish) to your shell init file. Your shell will have the color applied to it, and will watch `$XDG_RUNTIME_DIR/shellcolord/PID` for commands (`apply`, `disable` `enable`).

You can use `shellcolor` for sending commands. For example, `shellcolor apply` to apply the configured color to all watching shells. You can also specify its pid (`shellcolor disable $$`, for instance).

You can leverage this to disable color applying when ssh'ed to another machine, by running `shellcolor disable $$` before ssh, then `shellcolor enable $$ && shellcolor apply $$` after exiting.
