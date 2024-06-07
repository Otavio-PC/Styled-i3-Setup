# Getting Started with Ubuntu and i3-wm

This guide will help you set up Ubuntu with the i3 window manager quickly and easily.

## Prerequisites

You will need a Linux distribution. This guide uses Ubuntu 22.04.4 LTS and 24.04 LTS. Download the appropriate version from the [Ubuntu website](https://ubuntu.com/download/desktop).

Follow the official Ubuntu instructions to create a [bootable USB](https://ubuntu.com/tutorials/create-a-usb-stick-on-ubuntu#1-overview) and set up your machine with the necessary OS.

## Installation

1. **Update your system packages:**

    ```sh
    sudo apt update && sudo apt upgrade -y
    ```

2. **Install essential tools:**

    ```sh
    sudo apt install suckless-tools xclip maim
    ```

3. **Install i3 window manager:**

    ```sh
    sudo apt install i3-wm
    ```

4. **Install additional recommended packages:**

    ```sh
    sudo apt install i3status i3lock
    ```

5. **Optional: Install a terminal emulator (e.g., Terminator):**

    ```sh
    sudo apt install terminator
    ```

6. **Reboot your system:**

    ```sh
    sudo reboot
    ```

## Logging in with i3

1. At the Ubuntu login screen, go to the bottom right corner and click on the gear icon.
2. Select `i3` from the session options and then log in.

## Initial i3 Setup

1. After logging in with i3 for the first time, you will be prompted to generate a configuration file.
2. Choose "Yes, generate the config" and select `<Win> Win as default modifier`.

## Basic i3 Configuration

1. **Edit the i3 configuration file (optional):**

    The configuration file is located at `~/.config/i3/config`. You can edit this file to customize keybindings and other settings.

    ```sh
    nano ~/.config/i3/config
    ```

## Useful Keybindings

- `Win + Enter`: Open a terminal.
- `Win + D`: Launch application launcher (dmenu).
- `Win + 1-9`: Switch to workspace 1-9.
- `Win + Arrow keys`: Move focus to another window.
- `Win + Shift + 1-9`: Move focused window to workspace 1-9.
- `Win + Shift + Arrow keys`: Move the focused window within the workspace.
- `Win + Shift + Q`: Close the focused window.
- `Win + R`: Enter resize mode (use arrow keys to resize).
- `Win + Shift + C`: Restart i3 without rebooting the computer.

## Managing Old Kernels (Optional)

If you want to remove old kernel versions after installing Ubuntu:

1. **Check your current kernel version:**

    ```sh
    uname -r
    ```

    **Do not remove this version.**

2. **List all installed kernels:**

    ```sh
    dpkg --list 'linux-image-*'
    ```

3. **Remove old kernels:**

    ```sh
    sudo apt-get purge linux-image-x.x.x-x-generic
    ```

4. **Update GRUB:**

    ```sh
    sudo update-grub2
    ```

5. **Reboot your system:**

    ```sh
    sudo reboot
    ```

6. **If old kernels still appear in GRUB, you may need to clear the old partitions and resize your current partition. Afterward, update GRUB again:**

    ```sh
    sudo update-grub2 && sudo update-grub
    ```

    Reboot your system again to ensure the old kernels are no longer displayed.

## Resources

- [i3 User's Guide](https://i3wm.org/docs/userguide.html)
- [i3 FAQ](https://i3wm.org/docs/faq.html)

For further customization and advanced configurations, refer to the i3 documentation and community resources.



## Setting cool design
1. **Install cool-retro-term by:**
    ```bash
    sudo snap cool-retro-term --classic
    ```

2. **Install xclip and maim by ( needed for screenshot ):**
    ```bash
    sudo apt install xclip && sudo apt install maim
    ```

3. **Setting i3.config (copy and drag in config file):**

    ```
    ## Screenshots
    bindsym Print exec --no-startup-id maim "/home/$USER/Pictures/$(date)"
    bindsym $mod+Print exec --no-startup-id maim --window $(xdotool getactivewindow) "/home/$USER/Pictures/$(date)"
    bindsym Shift+Print exec --no-startup-id maim --select "/home/$USER/Pictures/$(date)"

    ## Clipboard Screenshots
    bindsym Ctrl+Print exec --no-startup-id maim | xclip -selection clipboard -t image/png
    bindsym Ctrl+$mod+Print exec --no-startup-id maim --window $(xdotool getactivewindow) | xclip  -selection clipboard -t image/png
    bindsym Ctrl+Shift+Print exec --no-startup-id maim --select | xclip -selection clipboard -t image/png
    ```
    find actual bind for $mod+Return and replace for:
    ```
    # start Cool-Retro-Terminal
    bindsym $mod+Return exec cool-retro-term
    ```

    Reboot your system.


## Setting Up Zsh for a Better Terminal Experience

1. **Install Zsh:**

    ```bash
    sudo apt install zsh -y
    ```

2. **Initial Configuration:**

    Unlike Bash and other shells, Zsh requires initial configuration when you start it for the first time. To start Zsh, type the following in the terminal and press Enter:

    ```sh
    zsh
    ```

3. **Set Zsh as the Default Shell:**

    After installation, Zsh is not configured and is not set as the default shell. To set Zsh as your default shell, follow these steps:

    ```sh
    chsh -s $(which zsh)
    ```

    You can verify the change by checking the value of the `$SHELL` variable:

    ```sh
    echo $SHELL
    ```

4. **Install Oh My Zsh:**

    Oh My Zsh is a framework for managing your Zsh configuration. Install it by running the following command:

    ```sh
    sh -c "$(wget https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh -O -)"
    ```

5. **Add a Custom Theme:**

    To customize the appearance of your terminal, you can change the Zsh theme. Open and edit the `.zshrc` configuration file using a text editor (e.g., nano):

    ```sh
    nano ~/.zshrc
    ```

    Locate the following line:

    ```sh
    ZSH_THEME="robbyrussell"
    ```

    Replace it with:

    ```sh
    ZSH_THEME="bira"
    ```

6. **Enable Auto-Suggestions:**

    Enable the auto-suggestions plugin to get command suggestions based on your Zsh command history. This saves time and helps you complete your daily tasks efficiently.

    ```sh
    git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
    ```

    Open the `.zshrc` configuration file:

    ```sh
    nano ~/.zshrc
    ```

    Add `zsh-autosuggestions` to the list of plugins:

    ```sh
    plugins=(git zsh-autosuggestions)
    ```

7. **Enable Syntax Highlighting:**

    Clone the syntax highlighting plugin repository:

    ```sh
    git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
    ```

    Open the `.zshrc` configuration file:

    ```sh
    nano ~/.zshrc
    ```

    Scroll down to the plugins section and add `zsh-syntax-highlighting` to the list of plugins:

    ```sh
    plugins=(git zsh-autosuggestions zsh-syntax-highlighting)
    ```

8. **Apply Changes:**

    Restart your terminal or apply the changes immediately by sourcing the `.zshrc` file:

    ```sh
    source ~/.zshrc
    ```


## Setting Up Styled Vim

1. **Installing vim:**

    ```bash
    sudo apt install vim && sudo apt-get install vim-gtk3
    ```

2. **Installing vim-plug plugin manager**

    To install vim-plug Plugin manager, all you have to do is run either one of the following commands:

    ```bash
    curl -fLo ~/.vim/autoload/plug.vim --create-dirs https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
    ```

2. **Move Font Files:**

   First, create a directory for the fonts and move the font files from the `Fonts` folder of this repository:

    ```bash
    mkdir ~/.fonts
    mv Fonts/*.ttf ~/.fonts
    ```

3. **Create and Configure `.vimrc`:**

    Create the `.vimrc` file in your user folder and add the following configurations. Each line includes a comment describing its purpose:

    ```vim
    " Initialize plugin system
    call plug#begin()

    " Fuzzy finder
    Plug 'junegunn/fzf', { 'do': { -> fzf#install() } }
    Plug 'junegunn/fzf.vim'

    " File system explorer
    Plug 'preservim/nerdtree'

    " Rust support
    Plug 'rust-lang/rust.vim'

    " Icons for various plugins
    Plug 'ryanoasis/vim-devicons'

    " Status/tab line
    Plug 'vim-airline/vim-airline'
    Plug 'vim-airline/vim-airline-themes'

    " Code formatting
    Plug 'prettier/vim-prettier', { 'do': 'yarn install --frozen-lockfile --production' }

    " End plugin system initialization
    call plug#end()

    " Set colors for end of buffer
    highlight EndOfBuffer ctermfg=black ctermbg=black

    " Set encoding to UTF-8
    set encoding=UTF-8

    " Set tab and shift width to 4 spaces
    set ts=4 sw=4

    " Enable mouse support in all modes
    set mouse=v

    " Show line numbers
    set number

    " Set number column width to 2
    set numberwidth=2

    " Improve command-line completion
    set cpoptions+=n

    " Use system clipboard
    set clipboard=unnamed

    " Set command for git grep
    set gp=git\ grep\ -n

    " Map Ctrl + A to select all
    map <C-a> <esc>ggVG<CR>

    " Map Ctrl + C to copy to system clipboard
    map <C-c> "+y<CR>

    " Keybindings for NERDTree
    nnoremap <leader>r :NERDTreeFocus<CR>:NERDTreeFind<CR> " \ + r => Refresh Tree
    nnoremap <leader>n :NERDTreeToggle<CR> " \ + n => Toggle Tree

    " Open terminal below with 10 rows
    nnoremap <leader>t :below terminal ++rows=10<CR>
    
    " Toggle mouse mode with F12
    map <silent><F12> :let &mouse=(&mouse == "a" ? "" : "a")<CR>:call ShowMouseMode()<CR>
    imap <silent><F12> :let &mouse=(&mouse == "a" ? "" : "a")<CR>:call ShowMouseMode()<CR>

    function ShowMouseMode()
        if (&mouse == 'a')
            echo "mouse-vim"
        else
            echo "mouse-xterm"
        endif
    endfunction

    " Enable airline tabline
    let g:airline#extensions#tabline#enabled = 1
    let g:airline#extensions#tabline#left_sep = ' '
    let g:airline#extensions#tabline#left_alt_sep = '|'
    let g:airline#extensions#tabline#formatter = 'unique_tail'

    " NERDTree arrows
    let g:NERDTreeDirArrowExpandable = "+"
    let g:NERDTreeDirArrowCollapsible = "~"

    " Enable powerline fonts for airline
    let g:airline_powerline_fonts = 1

    if !exists('g:airline_symbols')
        let g:airline_symbols = {}
    endif

    " Unicode symbols for airline
    let g:airline_left_sep = '»'
    let g:airline_right_sep = '«'
    let g:airline_symbols.linenr = '¶'
    let g:airline_symbols.branch = '⎇'
    let g:airline_symbols.paste = 'ρ'
    let g:airline_symbols.whitespace = 'Ξ'

    " Airline symbols
    let g:airline_left_sep = ''
    let g:airline_left_alt_sep = ''
    let g:airline_right_sep = ''
    let g:airline_right_alt_sep = ''
    let g:airline_symbols.branch = ''
    let g:airline_symbols.readonly = ''
    let g:airline_symbols.linenr = ''

    " Enable Unicode folder icons in NERDTree
    let g:WebDevIconsUnicodeDecorateFolderNodes = 1
    let g:WebDevIconsUnicodeDecorateFolderNodeDefaultSymbol = ''
    ```

4. **Save and Close the File:**

    Save and close the `.vimrc` file. In `vim`, you can do this by typing `:wq`.

5. **Install and Update Plugins:**

    Open `vim` and run the following commands to install and update the plugins:

    ```vim
    :PlugInstall
    :PlugUpdate
    ```

6. **Restart the Terminal:**

    After setting up Vim, close all terminal windows and reboot your machine for the changes to take effect.


## Setting Wallpapers and Changing Cool-Retro-Term Theme

1. **Installing feh:**

    To set wallpapers from the Sources/Wallpapers/ folder of this repository using feh, first, install feh:

    ```sh
    sudo apt install feh
    ```

2. **Using feh:**

    Then, use feh to set wallpapers. For example:

    ```sh
    feh --bg-scale path/to/your/image.jpg
    ```

    To ensure that the wallpaper is automatically set each time you start i3, add the following line to your i3 configuration file (~/.config/i3/config or ~/.i3/config):

    ```sh
    exec --no-startup-id feh --bg-scale /path/to/your/image.jpg
    ```

    Replace path/to/your/image.jpg with the actual path to your desired wallpaper image.


## Changing Cool-Retro-Term Theme:

To change the theme of Cool-Retro-Term, right-click on the terminal window and select "Settings". Then, import one of the themes located in the Sources/CRT_Themes/ folder of this repository by clicking on "Load". Alternatively, you can customize your own theme.


**This guide should provide a clear and organized path to set up Ubuntu with the i3 window manager. Adjust the steps as needed based on your specific requirements.**



