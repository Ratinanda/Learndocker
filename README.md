# Learndocker
# 1)Install the yum utils if not present
   yum install -y yum-utils
# 2) add the repo.
[root@AppServer ~]# yum-config-manager \
>     --add-repo \
>     https://download.docker.com/linux/centos/docker-ce.repo
bash: yum-config-manager: command not found...
Install package 'yum-utils' to provide command 'yum-config-manager'? [N/y] y


 * Waiting in queue...
The following packages have to be installed:
 libzstd-1.4.2-2.el8.x86_64     Zstd shared library
 yum-utils-4.0.12-4.el8_2.noarch        Yum-utils CLI compatibility layer
The following packages have to be updated:
 dnf-4.2.17-7.el8_2.noarch      Package manager
 dnf-data-4.2.17-7.el8_2.noarch Common data and configuration files for DNF
 dnf-plugins-core-4.0.12-4.el8_2.noarch Core Plugins for DNF
 libdnf-0.39.1-6.el8_2.x86_64   Library providing simplified C and Python API to libsolv
 librepo-1.11.0-3.el8_2.x86_64  Repodata downloading library
 libsolv-0.7.7-1.el8.x86_64     Package dependency solver
 python3-dnf-4.2.17-7.el8_2.noarch      Python 3 interface to DNF
 python3-dnf-plugins-core-4.0.12-4.el8_2.noarch Core Plugins for DNF
 python3-hawkey-0.39.1-6.el8_2.x86_64   Python 3 bindings for the hawkey library
 python3-libdnf-0.39.1-6.el8_2.x86_64   Python 3 bindings for the libdnf library.
 python3-librepo-1.11.0-3.el8_2.x86_64  Python 3 bindings for the librepo library
 python3-rpm-4.14.2-37.el8.x86_64       Python 3 bindings for apps which will manipulate RPM packages
 rpm-4.14.2-37.el8.x86_64       The RPM package management system
 rpm-build-libs-4.14.2-37.el8.x86_64    Libraries for building and signing RPM packages
 rpm-libs-4.14.2-37.el8.x86_64  Libraries for manipulating RPM packages
 rpm-plugin-selinux-4.14.2-37.el8.x86_64        Rpm plugin for SELinux functionality
 rpm-plugin-systemd-inhibit-4.14.2-37.el8.x86_64        Rpm plugin for systemd inhibit functionality
 yum-4.2.17-7.el8_2.noarch      Package manager
Proceed with changes? [N/y] y

# 3) install docker 

[root@AppServer ~]# yum install docker-ce docker-ce-cli containerd.io
Docker CE Stable - x86_64                                                                                                    347  B/s | 3.8 kB     00:11
Error:
 Problem 1: problem with installed package podman-docker-1.6.4-10.module_el8.2.0+305+5e198a41.noarch
  - package podman-docker-1.6.4-10.module_el8.2.0+305+5e198a41.noarch conflicts with docker-ce provided by docker-ce-3:19.03.13-3.el8.x86_64
  - conflicting requests
 Problem 2: problem with installed package podman-1.6.4-10.module_el8.2.0+305+5e198a41.x86_64
  - package podman-1.6.4-10.module_el8.2.0+305+5e198a41.x86_64 requires runc >= 1.0.0-57, but none of the providers can be installed
  - package containerd.io-1.3.7-3.1.el8.x86_64 conflicts with runc provided by runc-1.0.0-60.rc8.module_el8.1.0+237+63e26edc.x86_64
  - package containerd.io-1.3.7-3.1.el8.x86_64 obsoletes runc provided by runc-1.0.0-60.rc8.module_el8.1.0+237+63e26edc.x86_64
  - package containerd.io-1.3.7-3.1.el8.x86_64 conflicts with runc provided by runc-1.0.0-65.rc10.module_el8.2.0+305+5e198a41.x86_64
  - package containerd.io-1.3.7-3.1.el8.x86_64 obsoletes runc provided by runc-1.0.0-65.rc10.module_el8.2.0+305+5e198a41.x86_64
  - conflicting requests
  - package runc-1.0.0-64.rc10.module_el8.2.0+304+65a3c2ac.x86_64 is filtered out by modular filtering
(try to add '--allowerasing' to command line to replace conflicting packages or '--skip-broken' to skip uninstallable packages or '--nobest' to use not only best candidate packages)
[root@AppServer ~]# 
# 4) if error you can try below.how ever make sure you are not breaking something(at ur risk)
[root@AppServer ~]# yum install docker-ce docker-ce-cli containerd.io --allowerasing
Last metadata expiration check: 0:03:51 ago on Fri 30 Oct 2020 09:37:06 PM EDT.
Dependencies resolved.
=============================================================================================================================================================
 Package                         Architecture             Version                                                   Repository                          Size
=============================================================================================================================================================
Installing:
 containerd.io                   x86_64                   1.3.7-3.1.el8                                             docker-ce-stable                    29 M
     replacing  runc.x86_64 1.0.0-60.rc8.module_el8.1.0+237+63e26edc
 docker-ce                       x86_64                   3:19.03.13-3.el8                                          docker-ce-stable                    24 M
 docker-ce-cli                   x86_64                   1:19.03.13-3.el8                                          docker-ce-stable                    38 M
Installing dependencies:
 libcgroup                       x86_64                   0.41-19.el8                                               BaseOS                              70 k
Removing dependent packages:
 buildah                         x86_64                   1.9.0-5.module_el8.1.0+237+63e26edc                       @AppStream                          24 M
 podman                          x86_64                   1.6.4-10.module_el8.2.0+305+5e198a41                      @AppStream                          55 M
 podman-tests                    x86_64                   1.6.4-10.module_el8.2.0+305+5e198a41                      @AppStream                          76 k

Transaction Summary
=============================================================================================================================================================
Install  4 Packages
Remove   3 Packages

Total download size: 92 M
Is this ok [y/N]: y
Downloading Packages:
(1/4): libcgroup-0.41-19.el8.x86_64.rpm                                                                                       13 kB/s |  70 kB     00:05
(2/4): containerd.io-1.3.7-3.1.el8.x86_64.rpm                                                                                2.9 MB/s |  29 MB     00:10
(3/4): docker-ce-19.03.13-3.el8.x86_64.rpm                                                                                   2.0 MB/s |  24 MB     00:12
(4/4): docker-ce-cli-19.03.13-3.el8.x86_64.rpm                                                                               5.4 MB/s |  38 MB     00:07
-------------------------------------------------------------------------------------------------------------------------------------------------------------
Total                                                                                                                        5.1 MB/s |  92 MB     00:17
warning: /var/cache/dnf/docker-ce-stable-fa9dc42ab4cec2f4/packages/containerd.io-1.3.7-3.1.el8.x86_64.rpm: Header V4 RSA/SHA512 Signature, key ID 621e9f35: NOKEY
Docker CE Stable - x86_64                                                                                                    322  B/s | 1.6 kB     00:05
Importing GPG key 0x621E9F35:
 Userid     : "Docker Release (CE rpm) <docker@docker.com>"
 Fingerprint: 060A 61C5 1B55 8A7F 742B 77AA C52F EB6B 621E 9F35
 From       : https://download.docker.com/linux/centos/gpg
Is this ok [y/N]: y
Key imported successfully
Running transaction check
Transaction check succeeded.
Running transaction test
Transaction test succeeded.
Running transaction
  Preparing        :                                                                                                                                     1/1
  Running scriptlet: docker-ce-cli-1:19.03.13-3.el8.x86_64                                                                                               1/1
  Installing       : docker-ce-cli-1:19.03.13-3.el8.x86_64                                                                                               1/8
  Running scriptlet: docker-ce-cli-1:19.03.13-3.el8.x86_64                                                                                               1/8
  Installing       : containerd.io-1.3.7-3.1.el8.x86_64                                                                                                  2/8
  Running scriptlet: containerd.io-1.3.7-3.1.el8.x86_64                                                                                                  2/8
  Running scriptlet: libcgroup-0.41-19.el8.x86_64                                                                                                        3/8
  Installing       : libcgroup-0.41-19.el8.x86_64                                                                                                        3/8
  Running scriptlet: libcgroup-0.41-19.el8.x86_64                                                                                                        3/8
  Installing       : docker-ce-3:19.03.13-3.el8.x86_64                                                                                                   4/8
  Running scriptlet: docker-ce-3:19.03.13-3.el8.x86_64                                                                                                   4/8
  Erasing          : podman-tests-1.6.4-10.module_el8.2.0+305+5e198a41.x86_64                                                                            5/8
  Erasing          : podman-1.6.4-10.module_el8.2.0+305+5e198a41.x86_64                                                                                  6/8
  Running scriptlet: podman-1.6.4-10.module_el8.2.0+305+5e198a41.x86_64                                                                                  6/8
  Erasing          : buildah-1.9.0-5.module_el8.1.0+237+63e26edc.x86_64                                                                                  7/8
  Obsoleting       : runc-1.0.0-60.rc8.module_el8.1.0+237+63e26edc.x86_64                                                                                8/8
  Running scriptlet: runc-1.0.0-60.rc8.module_el8.1.0+237+63e26edc.x86_64                                                                                8/8
  Verifying        : libcgroup-0.41-19.el8.x86_64                                                                                                        1/8
  Verifying        : containerd.io-1.3.7-3.1.el8.x86_64                                                                                                  2/8
  Verifying        : runc-1.0.0-60.rc8.module_el8.1.0+237+63e26edc.x86_64                                                                                3/8
  Verifying        : docker-ce-3:19.03.13-3.el8.x86_64                                                                                                   4/8
  Verifying        : docker-ce-cli-1:19.03.13-3.el8.x86_64                                                                                               5/8
  Verifying        : buildah-1.9.0-5.module_el8.1.0+237+63e26edc.x86_64                                                                                  6/8
  Verifying        : podman-1.6.4-10.module_el8.2.0+305+5e198a41.x86_64                                                                                  7/8
  Verifying        : podman-tests-1.6.4-10.module_el8.2.0+305+5e198a41.x86_64                                                                            8/8

Installed:
  containerd.io-1.3.7-3.1.el8.x86_64      docker-ce-3:19.03.13-3.el8.x86_64      docker-ce-cli-1:19.03.13-3.el8.x86_64      libcgroup-0.41-19.el8.x86_64

Removed:
  buildah-1.9.0-5.module_el8.1.0+237+63e26edc.x86_64                               podman-1.6.4-10.module_el8.2.0+305+5e198a41.x86_64
  podman-tests-1.6.4-10.module_el8.2.0+305+5e198a41.x86_64

Complete!
[root@AppServer ~]#
# 4)start the docker service
[root@AppServer ~]# systemctl start docker
# 5) check the status of docker

[root@AppServer ~]# systemctl status docker
● docker.service - Docker Application Container Engine
   Loaded: loaded (/usr/lib/systemd/system/docker.service; disabled; vendor preset: disabled)
   Active: active (running) since Fri 2020-10-30 21:54:26 EDT; 8s ago
     Docs: https://docs.docker.com
 Main PID: 6331 (dockerd)
    Tasks: 8
   Memory: 42.6M
   CGroup: /system.slice/docker.service
           └─6331 /usr/bin/dockerd -H fd:// --containerd=/run/containerd/containerd.sock
# ======================================END=====================
