FROM minextu/mingw-sdl2:latest
MAINTAINER minextu

# install build tools
RUN pacman --noconfirm --needed -Sy \
        zip                 \
        emscripten          \
        python              \
        openssh          && \
    find /var/cache/pacman/pkg -mindepth 1 -delete

# install sdl
RUN pacman --noconfirm -Sy   \
        sdl2                 \
        sdl2_image           \
        sdl2_ttf          && \
    find /var/cache/pacman/pkg -mindepth 1 -delete

CMD /bin/bash
