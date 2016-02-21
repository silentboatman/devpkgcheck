# devpkgcheck

Tool that builds and tests pkgbuilds with vcs sources from the AUR.

## Usage

devpkgcheck is a great tool for verifying that your PKGBUILDs still builds correctly. Ideally from a cron job. It will fetch your vcs packages from the AUR, build them and run namcap. You will then get a warning if the build failed or if the namcap output changed from last build.

You can specifie your AUR user in two ways, either with the `-u` option or with a config setting. The `-q` option will only display info about packages with warnings or errors, thus perfect for a cron job.

It's also possible to fetch your PKGBUILDs from a local dir with the `-d` option.

```
devpkgcheck [options]

  -d, --dir <dir>        get pkgbuilds from a specified dir
  -h, --help             show this help message and exit
      --nocolor          disable colorized output messages
  -q, --quiet            show less information
  -u, --user <usr>       get pkg names from a specified AUR user
  -V, --version          show version and exit
```

The config file can be found at /etc/devpkgcheck.conf, but can also be copied to /home/user/.config/devpkgcheck.conf. It's possible to set the following variables in the config.
```
aur_user="foo_user"
ignore_pkgs="foo-git bar-git"
local_pkgdir="/home/user/pkgbuilds"
cache_dir="/home/user/.cache/devpkgcheck"
temp_dir="/temp/bar_folder"
```

## Example of crontab entry

```
* 3 * * 1 sudo -u user devpkgcheck --quiet --user "foo_user"
```
_note: When running devpkgcheck in crontab, you need to specify a user. That's because makepkg won't run as root._

## License

devpkgcheck is licensed under GPLv3.
