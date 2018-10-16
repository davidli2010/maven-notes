# GPG key generation: Not enough random bytes available.

Anyone who wants to create a new key set via GnuPG (GPG) may run into this error:

> We need to generate a lot of random bytes. It is a good idea to perform some other action (type on the keyboard, move the mouse, utilize the disks) during the prime generation; this gives the random number generator a better chance to gain enough entropy.
>
> Not enough random bytes available.  Please do some other work to give the OS a chance to collect more entropy! (Need 142 more bytes)

The problem is caused by the lack of entropy (or random system noise). While trying to get more, you might keep running into this message. In our case running a find on the disk, while making sha1sums and putting that into files, was actually not enough.

To check the available entropy, check the kernel parameters:

```bash
cat /proc/sys/kernel/random/entropy_avail
36
```

To solve the lack of entropy, we can use a random number generator utility like the rngd command

## Installation

Debian and Ubuntu: 

```bash
apt-get install rng-tools
```

Red Hat Enterprise Linux, Fedora, and CentOS: `yum install -y rng-tools` (or rng-utils on older systems)

Other distributions most likely will have the same package name available (rng-tools).

## Using rngd

```bash
rngd -f -r /dev/urandom
```

Checking the available entropy again revealed in our case a stunning 3100, almost 100 times more than before. GnuPG is now happy again and can finish creating the keys.
