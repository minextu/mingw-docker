FROM minextu/mingw-arch:latest
MAINTAINER minextu

#
# Installation of mingw-w64-sdl2 and sdl2-image
#

USER aur

# mingw-w64-sdl2
RUN yaourt -S --noconfirm --m-arg --nocheck    \
        mingw-w64-sdl2                      && \
    rm -r /tmp/* && sudo find /var/cache/pacman/pkg -mindepth 1 -delete

# mingw-w64-sdl2_image
RUN yaourt -S --noconfirm --m-arg --nocheck    \
        mingw-w64-sdl2_image                && \
    rm -r /tmp/* && sudo find /var/cache/pacman/pkg -mindepth 1 -delete

#
# Installation of mingw-w64-sdl2_ttf
#

# mingw-w64-freetype2-bootstrap
RUN yaourt -S --noconfirm --m-arg --nocheck --m-arg --skippgpcheck    \  
         mingw-w64-freetype2-bootstrap                             && \
    rm -r /tmp/* && sudo find /var/cache/pacman/pkg -mindepth 1 -delete

# mingw-w64-cairo-bootstrap
RUN yaourt -S --noconfirm --m-arg --nocheck --m-arg --skippgpcheck    \
        mingw-w64-cairo-bootstrap                                  && \
    rm -r /tmp/* && sudo find /var/cache/pacman/pkg -mindepth 1 -delete

# mingw-w64-harfbuzz
RUN yaourt -S --noconfirm --m-arg --nocheck --m-arg --skippgpcheck    \
        mingw-w64-harfbuzz                                         && \
    rm -r /tmp/* && sudo find /var/cache/pacman/pkg -mindepth 1 -delete

# mingw-w64-freetype2 (conflicts with freetype2-bootstrap)
RUN sudo pacman -Rdd mingw-w64-freetype2-bootstrap --noconfirm     && \
    yaourt -S --noconfirm --m-arg --nocheck --m-arg --skippgpcheck    \             
        mingw-w64-freetype2                                        && \
    rm -r /tmp/* && sudo find /var/cache/pacman/pkg -mindepth 1 -delete

# mingw-w64-sdl2_ttf
RUN yaourt -S --noconfirm --m-arg --nocheck --m-arg --skippgpcheck    \
        mingw-w64-sdl2_ttf                                         && \
    rm -r /tmp/* && sudo find /var/cache/pacman/pkg -mindepth 1 -delete

USER root
CMD /bin/bash
