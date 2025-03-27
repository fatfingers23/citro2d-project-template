# citro2d-project-template
This is an easy to use template for playing around with my work on [citro3d-rs](https://github.com/fatfingers23/citro3d-rs) to implement [citro2d](https://github.com/devkitPro/citro2d) with a safe Rust wrapper. At this moment you can only really draw 2D shapes, but the plan is to have a safe wrapper for all of citro2d.

The main is a direct copy of the [2d_shapes example](https://github.com/devkitPro/3ds-examples/tree/master/graphics/gpu/2d_shapes), but in Rust.

# Setup

## Setup ctru-rs/devkitARM toolchain
Follow the [ctru-rs setup guide](https://github.com/rust3ds/ctru-rs/wiki/Getting-Started) for setting up your dev environment.

Make sure you have the following environment variables set as well. The values depend on your devkitARM installation
```bash
export DEVKITPRO=/opt/devkitpro
export DEVKITARM=${DEVKITPRO}/devkitARM
export DEVKITPPC=${DEVKITPRO}/devkitPPC
```
You also need to make sure `$DEVKITPRO/tools/bin` and `$DEVKITARM/bin` in your path or you may see an error like `error: linker arm-none-eabi-gcc not found` on build
```bash
export PATH=${DEVKITPRO}/tools/bin:$PATH
export PATH=${DEVKITARM}/bin:$PATH

```


## VS Code setup with bacon ls
I did not have luck with using [rust analyzer as setup here](https://github.com/rust3ds/ctru-rs/wiki/Guides#setting-up-rust-analyzer) with my 3DS projects. But I found using bacon and bacon-ls helped a ton to keep a familiar workflow.

Although not strictly needed. I found having a [config.toml](.cargo/config.toml) setup helpful. Just make sure to update with the locations of your env variables for `DEVKITARM`


1. Make sure you have [bacon](https://github.com/Canop/bacon) installed `cargo install --locked bacon`
2. Make sure have [bacon-ls](https://github.com/crisidev/bacon-ls) installed `cargo install --locked bacon-ls`
3. Install the [VS Code extension](https://marketplace.visualstudio.com/items?itemName=MatteoBigoi.bacon-ls-vscode)
4. Usually need to set up a [bacon.toml](./bacon.toml) as explained [here](https://github.com/crisidev/bacon-ls?tab=readme-ov-file#configuration), but there is already one setup for this project.
5. You need to make sure bacon is running for it to work, can do that with `bacon -j bacon-ls`

## Running in an emulator
Once you build with `cargo 3ds build` it will print out the locations for a file ending in `.3dsx` this is found in your [target](./target/armv6k-nintendo-3ds/debug/) (link only works locally and after first build) folder. This is the file you open in the emulator.

Some options for emulators
* [Citra (rip)](https://citra-emulator.com/)
* [Lime3DS (archived)](https://github.com/Lime3DS/lime3ds-archive)
* [Azahar Emulator (Successor to lime-3ds)](https://github.com/azahar-emu/azahar)
* [Panda3DS (2D complex shapes do not show as well for some reason)](https://panda3ds.com/)

All of these can usually open a `3dsx` file via the command line. I usually like to have a just file like this for development
```justfile
shapes-example:
    cargo 3ds build
    lime3ds target/armv6k-nintendo-3ds/debug/citro2d-project-template.3dsx 
```


## Running on real hardware
To run on real hardware you need to have a modded 3DS running a custom firmware. The best way to do this is to follow the guides found at [3DS Hacks Guide](https://3ds.hacks.guide/). These are step by step for all models and versions.

1. Make sure your 3DS is connected to the same network as your computer.
2. Once you have your 3DS modded and the homebrew launcher installed open the homebrew launcher.
3. On the main screen of homebrew launcher press `Y` on your console and should see a screen that says "3dslink NetLoader" along with an IP address.
4. In the projects root run `cargo 3ds run --address {address from step 3}`
(May not need the `--address` flag depending on how your network is configured)
