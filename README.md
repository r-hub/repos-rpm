
# RPM packages for R-hub

## Current packages

* `JAGS 4.3.2` for Fedora 38, x86_64 and aarch64.

## Using this repository

## Updating

```
docker run -v `pwd`:/rpms -ti fedora:38 bash
```

```
yum install -y createrepo rpm-build rpm-sign wget gcc python3 yum-utils pinentry
```

```
gpg --import pgp-key.private
echo "%_signature gpg
%_gpg_name 2D0A34BD1C5AF134" > /root/.rpmmacros
```

```
export GPG_TTY=$(tty)
rpm --addsign /rpms/fedora-38/*.rpm
```

```
cd fedora-38
createrepo .
gpg --detach-sign --armor repodata/repomd.xml
```

## Thanks

[Creating and hosting your own rpm packages and yum repo](https://earthly.dev/blog/creating-and-hosting-your-own-rpm-packages-and-yum-repo/)
by Alex Couture-Beil @ https://earthly.dev/
