# vnStat in a snap - Experimental

**Note!** This snap should be considered experimental and isn't likely
the best way to install vnStat currently. See at least the limitations section below.

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

## Known limitations

- configuration file doesn't get exposed
- `vnstati` command  is `vnstat.image` instead
- `vnstat.image` can't write files due to snap sandbox restriction
  - use `-o - >file.png` as a workaround
- man pages aren't available
  - <https://forum.snapcraft.io/t/support-for-man-pages/2299>
  - <https://bugs.launchpad.net/snapd/+bug/1575593>
  - <https://github.com/snapcore/snapd/pull/8079>
