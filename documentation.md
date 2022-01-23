# Documentation

This document will contain the basic documentation for configuring my Arch distro. 

You can open terminal and run the below to download all of my configs and then run through the guide below, or you can pick and choose. 

`git clone https://gitlab.com/brandonlee712/configs.git`

That will download the entire repo.  If you want to place them in a nice and tidy location, I suggest Documents. so id you open terminal, prior to downloading the repo above and type 

`cd Documents`

 then run the above command, the repo will download into a folder called "configs" in your documents folder.

## Install Yay

open terminal and paste this into the terminal.  It will then install yay.  

`sudo pacman -S --needed git base-devel && git clone https://aur.archlinux.org/yay.git && cd yay && makepkg -si`

## Install Alacritty Terminal

Open terminal and type:

`sudo pacman -S alacritty`

# Ricing / Theming

### Install Dracula GTK Theme

you can do this from either the aur by opening alacritty terminal and typing 

`yay dracula-gtk-theme`

and selecting a corresponding number.  You'd then go through the prompts. 

### Activate The Theme

Now we need to activate the gtk theme. Every distribution is slightly different, Typically you can find an app built into the distro called "appearance" then once it is opened select "dracula." 

If you are using a de based on XFCE, if you open Alacritty and type 

`xfce4-appearance-settings`

and hit enter on your keyboard, it will open the application to set icons and gtk theme. 

### Download / Set Dracula Icons

Open Alacritty terminal and type:

`yay dracula-icons-git`

and hit enter on your keyboard. This will search the aur. You will likely only have 1 result returned so type 1  on your keyboard and go through the prompts. Once this is finished building you will have the Dracula theme icons downloaded. Now we need to set them. 

### Set Dracula Icons

As I said previously, every distribution will be a little different. In this case, I use XFCE so in Alacritty if I type 

`xfce4-appearance-settings` 

and hit enter on my keyboard, I can then select "icons" on the tabs and select Dracula. 

### X11 Resources

Open a web browser and paste this link and download the zip

`https://github.com/dracula/xresources/archive/master.zip`

unzip the content and copy the xresources file to your home directory. Then reboot your pc. 

### Dracula Theme for Alacritty

DistroTube's Derek Taylor had a slick way of setting various color schemes for Alacritty. I copied that section from his config, and then placed it into my config.  You can edit it freely, it's pretty understandable what you need to do once you begin looking around. 

To get Dracula theme, if you downloaded my configs repo just go into the download > alacritty/alacritty.yml and copy it to your .config/alacritty folder. If you have anything custom set, I suggest just copying it between the documents. 

### Set Dracula Wallpaper

*Note: You can obviously use any wallpaper you'd want. For this, I am going to use Dracula. you can go to my gitlab and download my wallpapers repo, or just find a wallpaper from the internet and save it, etc. it's up to you*

My gitlab for wallpapers is https://gitlab.com/brandonlee712/wallpapers

to clone it, I suggest cloning it in your Pictures directory 

open a terminal and type `cd Pictures`

if you want to clone my repo:

`git clone https://gitlab.com/brandonlee712/wallpapers.git`

this will download my wallpapers I've found online and you will easily be able to locate them to change your wallpaper. 

open a terminal and type `xfdesktop-settings`

on the backgrounds tab select the "folder" dropdown and navigate to "Pictures" and select the folder we cloned earlier (or a personal folder for wallpapers, etc). This will populate the box of previews for your wallpapers. Select the one you want.  Your wallpaper is now set. 

# Install NeoVim / Plugins

### Install Neovim

open Alacritty Terminal and type:

`sudo pacman -S neovim`

### Create Config

Make directory for Neovim Config

`mkdir ~/.config/nvim`

### Create `init.vim` file

`touch ~/.config/nvim/init.vim`

### Install Vim-Plug

Paste this into Alacritty Terminal

`curl -fLo ~/.config/nvim/autoload/plug.vim --create-dirs https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim`

You should have `plug.vim` in your autoload directory. 

### Add a new file for plugins

We will manage our plugins in a seperate file

`mkdir ~/.config/nvim/vim-plug`

`touch ~/.config/nvim/vim-plug/plugins.vim`

### Add Plugins

Add the below to `~/.config/nvim/vim-plug/plugins.vim`

```vim
" auto-install vim-plug
if empty(glob('~/.config/nvim/autoload/plug.vim'))
  silent !curl -fLo ~/.config/nvim/autoload/plug.vim --create-dirs
    \ https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
  "autocmd VimEnter * PlugInstall
  "autocmd VimEnter * PlugInstall | source $MYVIMRC
endif

call plug#begin('~/.config/nvim/autoload/plugged')

    " Better Syntax Support
    Plug 'sheerun/vim-polyglot'
    " File Explorer
    Plug 'scrooloose/NERDTree'
    " Auto pairs for '(' '[' '{'
    Plug 'jiangmiao/auto-pairs'

call plug#end()
```

### Source Plugins

Add the below to `init.vim`

`source $HOME/.config/nvim/vim-plug/plugins.vim`

### Vim-Plug Commands

Check the status of your plugins

`:PlugStatus`

Install all of your plugins

`:PlugInstall`

To update your plugins

`:PlugUpdate`

*Note:* After the update you can press `d` to see the differences or run

`:PlugDiff`

To remove plugins that are no longer defined in the `plugins.vim` file

`:PlugClean`

Finally if you want to upgrade vim-plug itself run the following

`:PlugUpgrade`

### Install Dracula Theme for NeoVim

We need to install the Dracula theme for Neovim (to match our Rice of course)

open `~/.config/nvim/vim-plug/plugins.vim` and paste in (under our other plugins on a new line)

```vim
" Dracula Theme
    Plug 'Mofiqul/dracula.nvim'
```

open ``~/.config/nvim/vim-plug/plugins.vim` and at the end paste

```vim
" Vim-Script:
colorscheme dracula
```

save and close. 
