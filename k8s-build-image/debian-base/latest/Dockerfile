# Copyright 2017 The Kubernetes Authors.
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#     http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

FROM cr.loongnix.cn/library/debian:buster

ARG ARCH

ENV DEBIAN_FRONTEND=noninteractive

# Smaller package install size.
COPY excludes /etc/dpkg/dpkg.cfg.d/excludes

# Convenience script for building on this base image.
COPY clean-install /usr/local/bin/clean-install

# An attempt to fix issues like:
# ```
# Error while loading /usr/sbin/dpkg-split: No such file or directory
# Error while loading /usr/sbin/dpkg-deb: No such file or directory
# ```
# See: https://github.com/docker/buildx/issues/495
RUN ln -s /usr/bin/dpkg-split /usr/sbin/dpkg-split && \
    ln -s /usr/bin/dpkg-deb /usr/sbin/dpkg-deb && \
    ln -s /bin/tar /usr/sbin/tar && \
    ln -s /bin/rm /usr/sbin/rm

# Update system packages.
RUN apt-get update \
    && apt-get dist-upgrade -y

# Hold required packages to avoid breaking the installation of packages
RUN apt-mark hold apt gnupg adduser passwd libsemanage1 libcap2

# Remove unnecessary packages.
# This list was generated manually by listing the installed packages (`apt list --installed`),
# then running `apt-cache rdepends --installed --no-recommends` to find the "root" packages.
# The root packages were evaluated based on whether they were needed in the container image.
# Several utilities (e.g. ping) were kept for usefulness, but may be removed in later versions.
# RUN echo "Yes, do as I say!" | apt-get purge \
#     bash \
#     e2fsprogs \
#     libcap2-bin \
#     libmount1 \
#     libsmartcols1 \
#     libblkid1 \
#     libss2 \
#     ncurses-base \
#     ncurses-bin \
#     tzdata

# No-op stubs replace some unnecessary binaries that may be depended on in the install process (in
# particular we don't run an init process).
WORKDIR /usr/local/bin
RUN touch noop && \
    chmod 555 noop && \
    ln -s noop runlevel && \
    ln -s noop invoke-rc.d && \
    ln -s noop update-rc.d
WORKDIR /

# Cleanup cached and unnecessary files.
RUN apt-get autoremove -y && \
    apt-get clean -y && \
    tar -czf /usr/share/copyrights.tar.gz /usr/share/common-licenses /usr/share/doc/*/copyright && \
    rm -rf \
        /usr/share/doc \
        /usr/share/man \
        /usr/share/info \
        /usr/share/locale \
        /var/lib/apt/lists/* \
        /var/log/* \
        /var/cache/debconf/* \
        /usr/share/common-licenses* \
        /usr/share/bash-completion \
        ~/.bashrc \
        ~/.profile \
        /etc/systemd \
        /lib/lsb \
        /lib/udev \
        /usr/lib/x86_64-linux-gnu/gconv/IBM* \
        /usr/lib/x86_64-linux-gnu/gconv/EBC* && \
    mkdir -p /usr/share/man/man1 /usr/share/man/man2 \
        /usr/share/man/man3 /usr/share/man/man4 \
        /usr/share/man/man5 /usr/share/man/man6 \
        /usr/share/man/man7 /usr/share/man/man8
