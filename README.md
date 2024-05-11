
# Updating 

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
```
