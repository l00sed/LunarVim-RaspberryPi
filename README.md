# Installing LunarVim on Raspberry Pi 4 (ARMv7)

1. Install Rust:
    `curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh`

2. Reboot your terminal, then check your install:
    `which rustup`
    `which cargo`

3. Install Node:
  - Check your ARM version:
    `cat /proc/cpuinfo`
  - On the Raspberry Pi 4, I had ARMv7
    - Download appropriate the binary [here](https://nodejs.org/en/download/), or use this (for ARMv7):
      `wget https://nodejs.org/dist/v16.15.1/node-v16.15.1-linux-armv7l.tar.xz`
      `sudo mkdir -p /usr/local/lib/nodejs`
      `sudo tar -xJvf node-v16.15.1-linux-armv7l.tar.xz -C /usr/local/lib/nodejs`

4. Set Node ENV variables in `~/.profile` or `~/.bashrc`
  `export PATH=/usr/local/lib/nodejs/node-v16.15.1-linux-armv7l/bin:$PATH`
  - Source your dotfile and then test:
    `node -v`

5. Install a C compiler
  `sudo apt-get install gcc`

6. Install tree-sitter-cli
  `cargo install tree-sitter-cli`

7. Install Neovim:
  - Install Pre-requisites:
  `sudo apt-get install ninja-build gettext libtool libtool-bin autoconf automake cmake g++ pkg-config unzip curl doxygen`
  `git clone https://github.com/neovim/neovim ~/Downloads/neovim`
  - There was an issue described here:
    https://neovim.discourse.group/t/has-anyone-been-able-to-get-neovim-0-7-0-to-work-on-aarch64/2386/4
  `cd ~/Downloads/neovim && make CMAKE_EXTRA_FLAGS="-DCOMPILE_LUA=OFF -DCMAKE_INSTALL_PREFIX=$HOME/neovim" CMAKE_BUILD_TYPE=RelWithDebInfo`
  `make install`
  `export PATH="$HOME/neovim/bin:$PATH"`
  - To uninstall, if you want:
    `sudo rm /usr/local/bin/nvim`
    `sudo rm -r /usr/local/share/nvim/`

8. Finally, install LunarVim ("Install In One Command!" ---my ass):
  `bash <(curl -s https://raw.githubusercontent.com/lunarvim/lunarvim/master/utils/installer/install.sh)`
