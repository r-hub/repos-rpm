
# RPM packages for R-hub

## Current packages

* `JAGS 4.3.2` for Fedora 38, x86_64 and aarch64:
  ```
  https://rpms.r-pkg.org/fedora-38/jags-4.3.2-1.aarch64.rpm
  https://rpms.r-pkg.org/fedora-38/jags-4.3.2-1.x86_64.rpm
  ```

## Using this repository

### Add the repository

Add the repository first:
```
curl -L -o /etc/yum.repos.d/rhub.repo https://rpms.r-pkg.org/fedora-38/rhub.repo
```

Then you can install packages as usual:
```
dnf install jags
```

### One off installs

For a one off installation, you don't need to add the repository.
You can use the URL to the RPM files (see above) directly. E.g.
```
dnf install -y https://rpms.r-pkg.org/fedora-38/jags-4.3.2-1.x86_64.rpm
```

## Updating

```
docker run -v `pwd`:/rpms -ti fedora:38 bash
```

```
yum install -y createrepo rpm-build rpm-sign wget gcc python3 yum-utils pinentry
```

```
cd /rpms
gpg --import pgp-key.private
echo "%_signature gpg
%_gpg_name 2D0A34BD1C5AF134" > /root/.rpmmacros
```

Copy or update the RPM files.

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
