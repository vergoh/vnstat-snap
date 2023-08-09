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

For more install options, see <https://snapcraft.io/vnstat>.

## Post install steps

The following needs to be executed once to provide the vnStat daemon access
to network interface speed details:

```sh
sudo snap connect vnstat:network-observe
sudo snap restart vnstat
```

Finally verify that the daemon did (re)start without issues:

```sh
sudo snap logs vnstat
```

## Configurability

Snap doesn't support using a configuration file in `/etc` or in the home directory
due to sandbox restrictions. Instead, Snap provides a configuration interface via
the `snap` command directly. For vnStat, the commands are:

- `sudo snap get vnstat` - list all configuration options and values
- `sudo snap set vnstat key=value` - set configuration option `key` with value `value`
- `sudo snap unset vnstat key` - restore default value of option `key`

All the configuration options in Snap mirror the same names as in the vnStat configuration
file but in full lower case. From vnStat's perspective, the active configuration can be
queried with `vnstat --showconfig`. A restart of the daemon is still needed when changing
daemon related configuration options. See the [vnstat.conf man page](https://humdi.net/vnstat/man/vnstat.conf.html)
for longer description for each option.

## Known limitations

- `vnstati` command is `vnstat.image` instead
- `vnstat.image` can't write files due to snap sandbox restriction
  - use `-o - >file.png` as a workaround
- man pages aren't available, use these these instead:
  - <https://humdi.net/vnstat/man/vnstat.html>
  - <https://humdi.net/vnstat/man/vnstati.html>
  - <https://humdi.net/vnstat/man/vnstat.conf.html>
- more details regarding lack of man pages in snaps:
  - <https://forum.snapcraft.io/t/support-for-man-pages/2299>
  - <https://bugs.launchpad.net/snapd/+bug/1575593>
  - <https://github.com/snapcore/snapd/pull/8079>
