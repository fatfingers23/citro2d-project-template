# citro2d-project-template


# Setup

## Setup ctru-rs/devkitARM toolchain
Follow the [ctru-rs setup guide](https://github.com/rust3ds/ctru-rs/wiki/Getting-Started) for setting up your dev environment.

## VS Code setup with bacon ls
1. Make sure you have [bacon](https://github.com/Canop/bacon) installed `cargo install --locked bacon`
2. Make sure have [bacon-ls](https://github.com/crisidev/bacon-ls) installed `cargo install --locked bacon-ls`
3. Install the [VS Code extension](https://marketplace.visualstudio.com/items?itemName=MatteoBigoi.bacon-ls-vscode)
4. Usually need to set up a [bacon.toml](./bacon.toml) as emplaned [here](https://github.com/crisidev/bacon-ls?tab=readme-ov-file#configuration), but there is already one setup for this project.
5. You need to make sure bacon is running for it to work, can do that with `bacon -j bacon-ls`

## Running in an emulator
Once you build with `cargo 3ds build` it will print out the locations for a file ending in `.3dsx` this is found in your [target](./target/armv6k-nintendo-3ds/debug/) (link only works locally and after first build) folder. This is the file you open in the emulator.

Some options for emulators
* [Citra (rip)](https://citra-emulator.com/)
* [Lime3DS (archived)](https://github.com/Lime3DS/lime3ds-archive)
* [Azahar Emulator (Succesor to lime-3ds)](https://github.com/azahar-emu/azahar)
* [Panda3DS (2D Circles do not show as well for some reason)](https://panda3ds.com/)

All of these can usually open a `3dsx` file via the command line. I usually like to have a just file like this for development
```justfile
shapes-example:
    cargo 3ds build --example system_font
    lime3ds target/armv6k-nintendo-3ds/debug/citro2d-project-template.3dsx 
```


## Running on real hardware
Draft
* Modded 3ds
* Homebrew press y
* Cargo 3ds run --address from homebrew