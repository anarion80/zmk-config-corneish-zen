# anarion's zmk config

This is my personal ZMK firmware configuration. It consists of a 42-keys base layout that I use with my Corne-ish Zen keyboard.

It is using excellent [zmk-config](https://github.com/urob/zmk-config) from [urob](https://github.com/urob) with only small modifications.

I switched from QMK, where even with also excellent [Bi-lateral combinations](https://sunaku.github.io/home-row-mods.html) and [multi-mod crossover chords](https://github.com/manna-harbour/qmk_firmware/pull/56) by [sunaku](https://sunaku.github.io) I could not type fast enough with Home Row Mods without accidently triggering them. With urob's pack of PRs - no issue!

To build this I use urob's [personal zmk fork](https://github.com/urob/zmk/tree/main-with-native-mouse) from the branch with native mouse support.

First I follow the [zmk toolchain setup](https://zmk.dev/docs/development/setup):

1. Open [personal zmk fork](https://github.com/urob/zmk/tree/main-with-native-mouse) in devcontainer.
2. `west init -l app/`
3. `west update`
4. `west zephyr-export`
5. `pip3 install -r zephyr/scripts/requirements.txt`
6. Stop the container by exiting VSCode.
7. Remove the docker container.
8. Remove the `zmk-config` volume.
9. Bind the `zmk-config` volume to the correct path pointing to your local zmk-config folder: `docker volume create --driver local -o o=bind -o type=none -o device="/mnt/c/Users/anarion/Documents/repos/zmk-config-porcupine-anarion/" zmk-config`
10. Start VSCode and rebuild the container.
11. `cd app/`
12. `west build -d build/corneish_left -b corneish_zen_v1_left -- -DZMK_CONFIG="/workspaces/zmk-config/config"`
13. `west build -d build/corneish_right -b corneish_zen_v1_right -- -DZMK_CONFIG="/workspaces/zmk-config/config"`
14. Flash the files.

<img src="img/corneish_zen.svg" alt="anarion's keymap layout graphical representation" width="100%" />

> Drawn with [Keymap Drawer](/caksoylar/keymap-drawer)
