# latency-obfuscator
This daemon is intended to mitigate various timing
attacks. It was created in particular to mitigate a covert channel based on the
observation that ping latency is caused by C-state transitions triggered by CPU usage
patterns.
 
# Mechanism

tc-netem is initialized for every active NIC and a random delay is applied 
per packet. The delay value is chosen randomly from an interval specified as a command-line
argument using Linux's PRNG with a default range of 75-200ms. This should make it very
difficult to observe timing differences even up the order of 100 ms.
For larger timing differences, the default interval isn't adequate and should be
increased in both magnitude and range.

Per-packet as opposed to per-slot delays were chosen because inter-packet timing differences can 
still survive in a group of sequestered packets and assist an attacker.


See also: https://phabricator.whonix.org/T530
## How to install `latency-obfuscator` using apt-get ##

1\. Download [Whonix's Signing Key]().

```
wget https://www.whonix.org/patrick.asc
```

Users can [check Whonix Signing Key](https://www.whonix.org/wiki/Whonix_Signing_Key) for better security.

2\. Add Whonix's signing key.

```
sudo apt-key --keyring /etc/apt/trusted.gpg.d/whonix.gpg add ~/patrick.asc
```

3\. Add Whonix's APT repository.

```
echo "deb https://deb.whonix.org buster main contrib non-free" | sudo tee /etc/apt/sources.list.d/whonix.list
```

4\. Update your package lists.

```
sudo apt-get update
```

5\. Install `latency-obfuscator`.

```
sudo apt-get install latency-obfuscator
```

## How to Build deb Package from Source Code ##

Can be build using standard Debian package build tools such as:

```
dpkg-buildpackage -b
```

See instructions. (Replace `generic-package` with the actual name of this package `latency-obfuscator`.)

* **A)** [easy](https://www.whonix.org/wiki/Dev/Build_Documentation/generic-package/easy), _OR_
* **B)** [including verifying software signatures](https://www.whonix.org/wiki/Dev/Build_Documentation/generic-package)

## Contact ##

* [Free Forum Support](https://forums.whonix.org)
* [Professional Support](https://www.whonix.org/wiki/Professional_Support)

## Donate ##

`latency-obfuscator` requires [donations](https://www.whonix.org/wiki/Donate) to stay alive!
