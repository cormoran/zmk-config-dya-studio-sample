# cormoran's ZMK config template

![ZMK Version](https://img.shields.io/badge/ZMK-master-blue)
[![Build ZMK firmware](https://github.com/cormoran/zmk-config-template/actions/workflows/build.yml/badge.svg)](https://github.com/cormoran/zmk-config-template/actions/workflows/build.yml)

After forking, replace all string `cormoran/zmk-config-template` with yours.

## Development

### Setup

The template supports two directory layouts `config/west-isolated.yml` (default) and `config/west-workspace.yml`.

```bash
mkdir zmk-workspace
cd zmk-workspace
git clone git@github.com:cormoran/zmk-config-template.git
cd zmk-config-template
west init -l config # It downloads dependencies to zmk-workspace/zmk-config-template/dependencies
# Or
# west init -l . --mf config/west-workspace.yml # It downloads dependencies under zmk-workspace/
west update --narrow
west zephyr-export
```

### Build

The build uses custom west commands provided by [comoran/zmk-west-commands](https://github.com/cormoran/zmk-west-commands).

```bash
# Build all artifacts
west zmk-build

# Build with debug
west zmk-build -S zmk-usb-logging

# Build specific firmware with debug mode and flash
west zmk-build -a <artifact name> -S zmk-usb-logging --flash
```

The build also runs once per week on CI by default to verify with the latest zmk version.

### Release

Pre-defined actions supports releasing firmware like [cormoran/zmk-config-template@v0.3.0.0](https://github.com/cormoran/zmk-config-template/releases/tag/v0.3.0.0).

1. Enable Settings > Actions > Workflow permissions > Read and write permissions
2. Execute "Build ZMK firmware" job from Actions > Run workflow with filling version like `v1.0.0`

## Keymap

[![Draw ZMK keymaps](https://github.com/cormoran/zmk-config-template/actions/workflows/draw-keymap.yml/badge.svg)](https://github.com/cormoran/zmk-config-template/actions/workflows/draw-keymap.yml)

![Your keymap](./keymap-drawer/your_keyboard.svg)
