# XDG [![Go Report Card](https://goreportcard.com/badge/github.com/j4ns8i/xdg)](https://goreportcard.com/report/github.com/j4ns8i/xdg) [![GoDoc](https://godoc.org/github.com/j4ns8i/xdg?status.svg)](https://godoc.org/github.com/j4ns8i/xdg)

A cross platform package that tries to follow [XDG
Standard](https://specifications.freedesktop.org/basedir-spec/basedir-spec-latest.html)
when possible. This repo is a fork of https://github.com/OpenPeeDeeP/xdg, which
chooses established MacOS directories over the defaults XDG mentioned in the
specification.

## Locations Per OS

The following table shows what is used if the envrionment variable is not set. If the variable is set then this package uses that. Unix derivatives follow the default standards. As for Windows, the variable defaults are just other environment variables set up by the operation system.

> When creating `XDG` application the `Vendor` and `Application` names are appeneded to the end of the path to keep projects unique.

|                   | Unix and Linux                     | Windows          |
| ---:              | :---:                              | :---:            |
| `XDG_DATA_DIRS`   | [`/usr/local/share`, `/usr/share`] | `%PROGRAMDATA%`  |
| `XDG_DATA_HOME`   | `~/.local/share`                   | `%APPDATA%`      |
| `XDG_CONFIG_DIRS` | [`/etc/xdg`]                       | `%PROGRAMDATA%`  |
| `XDG_CONFIG_HOME` | `~/.config`                        | `%APPDATA%`      |
| `XDG_CACHE_HOME`  | `~/.cache`                         | `%LOCALAPPDATA%` |

## Notes

- This package does not merge files if they exist across different directories.
- The `Query` methods search through the system variables, `DIRS`, first (when using environment variables first in the variable has presidence). It then checks home variables, `HOME`.
- This package will not create any directories for you. In the standard, it states the following:

> If, when attempting to write a file, the destination directory is non-existant an attempt should be made to create it with permission `0700`. If the destination directory exists already the permissions should not be changed. The application should be prepared to handle the case where the file could not be written, either because the directory was non-existant and could not be created, or for any other reason. In such case it may chose to present an error message to the user.
