# vnStat in a snap

vnStat is a network traffic monitor that uses the network
interface statistics provided by the kernel as information source. This
means that vnStat won't actually be sniffing any traffic and also ensures
light use of system resources regardless of network traffic rate.

By default, traffic statistics are stored on a five minute level for the last
48 hours, on a hourly level for the last 4 days, on a daily level for the
last 2 full months and on a yearly level forever. The data retention durations
are fully user configurable. Total seen traffic and a top days listing is also
provided.

See the [official webpage](https://humdi.net/vnstat/) or the
[GitHub repository](https://github.com/vergoh/vnstat) for additional details
and output examples. An example of the included image output is also
[available](https://humdi.net/vnstat/cgidemo/).

## How to install

Using release channel:

```sh
sudo snap install vnstat
```

Or alternatively using development channel:

```sh
sudo snap install vnstat --edge
```

vnStat will automatically start monitoring all available interfaces once installed. Statistics
can be viewed using the `vnstat` command (`sudo` not required) after around 5 minutes.

For more install options, see <https://snapcraft.io/vnstat>.
For more details about channels and versions, see the "Channels and versions" section below.

## Configurability

Snap doesn't support using a configuration file in `/etc` or in the home directory
due to sandbox restrictions. Instead, Snap provides a configuration interface via
the `snap` command directly. For vnStat, the commands are:

- `sudo snap get vnstat` - list all configuration options and values
- `sudo snap set vnstat key=value` - set configuration option `key` with value `value`
- `sudo snap unset vnstat key` - restore default value of option `key`

All the configuration options in Snap mirror the same names as in the vnStat configuration
file but in full lower case. From vnStat's perspective, the active configuration can be
queried with `vnstat --showconfig`. A restart of the daemon (`sudo snap restart vnstat`)
is needed after changing daemon related configuration options. See the
[vnstat.conf man page](https://humdi.net/vnstat/man/vnstat.conf.html) for longer descriptions
of each option.

## Known limitations

- `vnstati` (image output) command is available as `vnstat.image`
- `vnstat.image` can't write files due to snap sandbox restriction
  - use `-o - >file.png` as a workaround
- `sudo snap restart vnstat` is required after changing daemon related configuration options
- man pages aren't available, use these these instead:
  - <https://humdi.net/vnstat/man/vnstat.html>
  - <https://humdi.net/vnstat/man/vnstati.html>
  - <https://humdi.net/vnstat/man/vnstat.conf.html>
- more details regarding lack of man pages in snaps:
  - <https://forum.snapcraft.io/t/support-for-man-pages/2299>
  - <https://bugs.launchpad.net/snapd/+bug/1575593>
  - <https://github.com/snapcore/snapd/pull/8079>

## Channels and versions

vnStat is published on two snap channels:

- `latest/stable` - tracks the latest [vnStat release](https://github.com/vergoh/vnstat/releases)
  - `snap` defaults to using this channel when none is specified
  - the version string consists of two `-` separated fields:
    1. vnStat release version
    2. commit identifier for current repository
- `latest/edge` - tracks the latest all tests passing commit in the [vnStat GitHub repository](https://github.com/vergoh/vnstat)
  - can be selected using the `--edge` parameter
  - the version string consists of four `-` separated fields:
    1. vnStat release version
    2. number of commits after the above version
    3. commit identifier of the latest change
    4. commit identifier for current repository

In addition, with `snap list` command, a revision is visible. This revision is a unique incremental
identifier for the build being used. It will be incremented for any `vnstat` snap builds regardless of
channel or architecture.
