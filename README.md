## Motivation
Need the x11 forward fesature for slrum with open-HPC installation.

## how to compile (Centos 7.3 tested)

yum install rpmbuild

mkdir -p ~/rpmbuild/{BUILD,BUILDROOT,RPMS,SOURCES,SPECS,SRPMS}

git clone https://github.com/RichardAnthoyFalzini/slurm-spank-x11.git

```
tar  -zcf slurm-spank-x11-0.2.5.tar.gz slurm-spank-x11-0.2.5
mv slurm-spank-x11-0.2.5.tar.gz ~/rpmbuild/SOURCES/
cp slurm-spank-x11/slurm-spank-x11.spec ~/rpmbuild/SPECS/
```

vim /usr/lib/rpm/find-debuginfo.sh:
```
  while [ $# -gt 0 ]; do
    case "$1" in
    --strict-build-id)
      strict=true
      ;;
 ```
  BECOME
```
  while [ $# -gt 0 ]; do
    case "$1" in
    --strict-build-id)
      strict=false
      ;;
```
rpmbuild -v -ba ~/rpmbuild/SPECS/slurm-spank-x11.spec

if no error occurre you can find the rpm on:
  ~/rpmbuild/RPMS/x86_64/slurm-spank-x11-0.2.5-1.x86_64.rpm

if you whish you can ripristinate the file /usr/lib/rpm/find-debuginfo.sh

## Install 
has to be done on all nodes, frontend and compute
ensure that the file /etc/slurm/plugstack.conf exist and contain the line
```
  include /etc/slurm/plugstack.conf.d/*
```
then

  rpm --install ~/rpmbuild/RPMS/x86_64/slurm-spank-x11-0.2.5-1.x86_64.rpm

## Tests





