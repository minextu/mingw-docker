FROM archlinux/base
MAINTAINER minextu

# install build tools
RUN pacman --noconfirm --needed -Syu \
        cmake                 \
        git                   \
        base-devel            \
        wget

#
# AUR preparations
#

RUN echo 'aur ALL=(ALL) NOPASSWD: ALL' >> /etc/sudoers && useradd -m aur

# package-query
USER aur
RUN cd /tmp && \
    wget https://aur.archlinux.org/cgit/aur.git/snapshot/package-query.tar.gz && \
    tar -xvf package-query.tar.gz  && \
    cd package-query               && \
    makepkg -si --noconfirm        && \
    rm -r /tmp/*

# yaourt
RUN cd /tmp && \
    wget https://aur.archlinux.org/cgit/aur.git/snapshot/yaourt.tar.gz && \
    tar -xvf yaourt.tar.gz   && \
    cd yaourt                && \
    makepkg -si --noconfirm  && \
    rm -r /tmp/*

#
# Installation of the mingw-w64 base
#

# mingw-w64-binutils
RUN yaourt -S --noconfirm --m-arg --nocheck --m-arg --skippgpcheck    \
        mingw-w64-binutils                                         && \
    rm -r /tmp/*

# mingw-w64-headers
RUN yaourt -S  --noconfirm --m-arg --nocheck --m-arg --skippgpcheck    \
        mingw-w64-headers mingw-w64-headers-bootstrap               && \
    rm -r /tmp/*

# mingw-w64-gcc-base
RUN yaourt -S --noconfirm --m-arg --nocheck --m-arg --skippgpcheck    \
         mingw-w64-gcc-base                                        && \
    rm -r /tmp/*

# mingw-w64-crt
RUN yaourt -S --noconfirm --m-arg --nocheck --m-arg --skippgpcheck    \
        mingw-w64-crt                                              && \
    rm -r /tmp/*

# mingw-w64-winpthreads (mingw-w64-headers-bootstrap is conflicting)
RUN sudo pacman -Rdd --noconfirm mingw-w64-headers-bootstrap       && \
    yaourt -S --noconfirm --m-arg --nocheck --m-arg --skippgpcheck    \
        mingw-w64-winpthreads                                      && \
    rm -r /tmp/*

# mingw-w64-gcc (mingw-w64-gcc-base is conflicting)
RUN sudo pacman -Rdd --noconfirm mingw-w64-gcc-base                && \
    yaourt -S --noconfirm --m-arg --nocheck --m-arg --skippgpcheck    \            
        mingw-w64-gcc                                              && \
    sudo pacman -Rs --noconfirm gcc-ada                            && \
    rm -r /tmp/*

USER root
CMD /bin/bash
