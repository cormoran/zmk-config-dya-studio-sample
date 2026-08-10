# DYA Studio sample ZMK config

段階的に [DYA Studio 開発者ガイド](https://dya-studio-dev.cormoran707.workers.dev/developer-guide)
の各機能を導入する、キーボード制作者向けの参照実装です。

最初のコミットでは、Seeed Studio XIAO nRF52840 と組み合わせる非分割の
`dya_studio_sample` shield を定義します。ハードウェア構成は direct input の
4キーだけです。PMW3610 の配線・ドライバ・Studio 設定は Trackball のステップで
追加します。

| Component | Pins |
| --- | --- |
| 4 direct-input switches | XIAO D0, D1, D2, D3 |
| PMW3610 SCK | XIAO D5 (P0.05) — Trackball step |
| PMW3610 SDIO (MOSI/MISO) | XIAO D8 (P1.13) — Trackball step |
| PMW3610 motion interrupt | XIAO D9 (P1.14) — Trackball step |
| PMW3610 chip select | XIAO D10 (P1.15) — Trackball step |

## Tutorial commits

| Developer guide | Sample commit |
| --- | --- |
| [Level 1: ZMK Studio](https://dya-studio-dev.cormoran707.workers.dev/developer-guide/level-1) | `feat: enable official ZMK Studio` |
| [Level 2: DYA extensions](https://dya-studio-dev.cormoran707.workers.dev/developer-guide/level-2) | `feat: add DYA Studio protocol baseline` |
| [Keymap / Macro / Combo](https://dya-studio-dev.cormoran707.workers.dev/developer-guide/modules/keymap) | `feat: add editable keymap modules` |
| [Trackball](https://dya-studio-dev.cormoran707.workers.dev/developer-guide/modules/trackball) | `feat: add editable PMW3610 controls` |
| [Connection](https://dya-studio-dev.cormoran707.workers.dev/developer-guide/modules/connection) | `feat: add connection and OS controls` |
| [Settings](https://dya-studio-dev.cormoran707.workers.dev/developer-guide/modules/settings) | `feat: expose settings in DYA Studio` |
| [Diagnostics](https://dya-studio-dev.cormoran707.workers.dev/developer-guide/modules/diagnostics) | `feat: add DYA Studio diagnostics` |

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
