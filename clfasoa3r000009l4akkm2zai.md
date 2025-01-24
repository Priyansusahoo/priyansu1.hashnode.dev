---
title: "Fedora Linux SetUp"
datePublished: Thu Mar 16 2023 07:33:24 GMT+0000 (Coordinated Universal Time)
cuid: clfasoa3r000009l4akkm2zai
slug: fedora-linux-setup
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/MU8w72PzRow/upload/fbb13b419abcbad318521211bf4daef9.jpeg
tags: linux, fedora, linux-for-beginners, linux-basics, wemakedevs

---

## Install and Backup(*Setup*):

**NOTE:**

1. In Fedora, the `sub-volumes` are named in a specific way which is why `Time-shift` doesn’t work.
    
2. `Timeshift` works best with the Ubuntu style named `sub-volumes`.
    
3. Sub-volume names (Default) :
    

* root →(`/`)
    
* home →(`/home`)
    
    For time-shift to work we need to change the names of the sub-volumes.
    
* root→ (`@`)
    
* home→ (`@home`)
    

**STEPS:**

1. (a) Make volumes as given in the Snapshot & Add `SWAP` → extra. By clicking → *Click here to* ***create them automatically***.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1678948467620/e5a0880d-e38d-4f1f-b186-e95442d2a069.png align="center")
    

**OR**

**(b) Create partition Manually:**

* Add `/boot` about `1024 MiB`
    
* Add `/boot/efi` about `100 MiB`
    
* Add `SWAP` about `8 GiB`
    
* Add `/`root partition of size → Varies(`X GiB`)
    
    > Important:
    > 
    > change the Name: of the sub-volume from: *root → @*
    
* Add `/home` home partition of size → Same as `/`(root) i.e (`X GiB`).
    
    > Important:
    > 
    > change the Name: of the sub-volume from: */home → @home*
    

1. Accept Changes
    
2. Begin Installation
    
3. WAIT FOR THE INSTALLATION TO FINISH
    
4. Reboot the system
    
5. Now setup using the Setup Wizard
    

* Start Setup
    
* Privacy
    
    * Location Sevices (**turn off**)
        
    * Automatic Problem Reporting (**turn off**)
        
* Third-Party Repositories (**Enable**)
    
* Skip Online Account Creation
    
* Create login Id & password
    
* Continue using Fedora
    

### Configuration for SSD:

1. Go to the terminal:
    

> `cat /etc/fstab` `#check the fstab`

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1678948591591/6310936b-fcdc-4eaa-b648-8d5d963c2e4e.png align="left")

1. Configuration for SSD:
    

```bash
sudo nano /etc/fstab
# Input password

#Add the same line of code to the file in (**/)** & (**/home)** section
#Line of code:
compress=zstd,noatime,space_cache=v2,ssd,discard=async,
```

*For Reference*:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1678948681765/8e896222-3b58-4291-8a52-cb0e11ed57be.png align="left")

* now Save the files (`Ctrl + o`)and Exit (`Ctrl + x`).
    
* Reboot the system (`reboot`)
    
* The system should reboot just fine.
    

# After Installation Setup:

* \[**Change Touchpad settings** (`Tap to Click`)(`scrolling`) **and Add Shortcut keys (Setting, Home-folder, Terminal)** \]
    

1. **configure** `dnf`:
    

> `sudo nano /etc/dnf/dnf.conf`
> 
> Add:
> 
> ```bash
> gpgcheck=1
> installonly_limit=3
> clean_requirements_on_remove=True
> best=False
> skip_if_unavailable=True
> fastestmirror=true
> deltarpm=true
> max_parallel_downloads=7
> defaultyes=1
> ```

2. **Time-Shift Configure:**
    

```bash
sudo dnf check-update
sudo dnf install timeshift
```

* RSYNC
    
* Select disk (The disk should be of type: *btrfs* )
    
* Select Snapshot Levels:
    
    * Monthly → 2
        
    * Weekly → 3
        
    * Daily → 3
        
    * Boot → 2
        
* Exclude *@home*
    
* Enable BTRFS groups (recommended)→ if option available
    
* Finish
    
* Take a snapshot for backup purposes (*Recommended*)
    
    1. **Update the system:**
        

```bash
sudo dnf update
sudo dnf upgrade --refresh
```

1. **Enable** `RPM Fusion` Repository:
    

> free, non-free, other repository:

```bash
sudo rpm -Uvh http://download1.rpmfusion.org/free/fedora/rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm

sudo rpm -Uvh http://download1.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-$(rpm -E %fedora).noarch.rpm

sudo dnf groupupdate core

sudo dnf install -y rpmfusion-free-release-tainted

sudo dnf install -y dnf-plugins-core
```

* Reboot the system
    

```bash
sudo reboot now
```

1. **Update:**
    

> **Install** `updates` :

```bash
sudo dnf upgrade --refresh
sudo dnf check
sudo dnf autoremove
sudo fwupdmgr get-devices
sudo fwupdmgr refresh --force
sudo fwupdmgr get-updates
sudo fwupdmgr update
```

1. **Gnome Extensions and** `Tweaks`:
    

```bash
sudo dnf install -y gnome-extensions-app gnome-tweaks
#sudo dnf install -y gnome-shell-extension-appindicator
```

> **Enable Minimize or Maximize Button in Gnome-tweaks**

> *Install extensions from Firefox*:

* [**Sound Input & Output Device Chooser**](https://extensions.gnome.org/extension/906/sound-output-device-chooser/)
    
* User theme
    
* Dash to Dock
    
* Frippery application menu
    
    `Flatpak` support:
    

```bash
flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo

flatpak update
```

`Snap` support

```bash
sudo dnf install -y snapd

sudo ln -s /var/lib/snapd/snap /snap
```

* logout from the session
    

```bash
sudo snap refresh
```

1. **Configure** `Git`:
    

```bash
git config --global user.name "github-username"

git config --global user.email "github-user-email-address"
```

1. **Create** `.ssh` folder:
    

```bash
cd
mkdir ~/.ssh
cd ~/.ssh
```

1. **SSH keys:**
    

```bash
ssh-keygen -t ed25519 -C "github-user-email-address"

eval "$(ssh-agent -s)"

ssh-add ~/.ssh/id_ed25519
```

1. **Adding SSH in GitHub**:
    

* go to `.ssh` folder in the terminal (in the local machine)
    
* And copy the SSH key using Cat Command
    

```bash
cd ~/.ssh
cat id_ed25519.pub   #copy content
```

* Go to [GitHub](https://github.com/)
    
* Go to → [Settings](https://github.com/settings/profile)
    
* Then → [SSH and GPG Keys](https://github.com/settings/keys)
    
* Click → **Add New SSH**
    
* Paste the content below
    
    1. **Clone the required repository if needed.**
        
    2. **Microsoft Fonts (<mark>Warning: Takes ages to install</mark>)(<mark>optional</mark>)**
        

```bash
sudo dnf install -y curl cabextract xorg-x11-font-utils fontconfig

sudo rpm -i https://downloads.sourceforge.net/project/mscorefonts2/rpms/msttcore-fonts-installer-2.6-1.noarch.rpm
```

1. **System monitor & cleaning tool:**
    

```bash
sudo dnf install htop bpytop

sudo dnf install bleachbit
```

1. **Multimedia Codecs:**
    

```bash
sudo dnf install -y vlc # prefered

sudo dnf groupupdate sound-and-video

sudo dnf install -y libdvdcss

sudo dnf install -y gstreamer1-plugins-{bad-\*,good-\*,ugly-\*,base} gstreamer1-libav --exclude=gstreamer1-plugins-bad-free-devel ffmpeg gstreamer-ffmpeg 

sudo dnf install -y lame\* --exclude=lame-devel

sudo dnf group upgrade --with-optional Multimedia
```

1. For OpenH264 in Firefox I run:
    

```bash
sudo dnf config-manager --set-enabled fedora-cisco-openh264

sudo dnf install -y gstreamer1-plugin-openh264 mozilla-openh264
```

> Afterwards you need to open Firefox, go to menu → Add-ons → Plugins and enable OpenH264 plugin. You can do a simple test whether your H.264 works in RTC on this [page](https://mozilla.github.io/webrtc-landing/pc_test.html)  (check Require H.264 video).

```bash
# change Host Name:
sudo hostnamectl set-hosetname "fedora"
```

1. **To Install / Remove Essential Applications:**
    

```bash
#search:
dnf search <package_name>

snap search <package_name>

sudo dnf install <package_name>

sudo snap install <package_name>

sudo dnf remove <package_name>
```

1. **Screen Lock and Power Settings**
    
2. **Use Night Light Settings**
    

# Install Applications

1. Notion
    

```bash
sudo snap install notion-snap
```

1. Sublime Text:
    

```bash
# Install GPG key:
sudo rpm -v --import https://download.sublimetext.com/sublimehq-rpm-pub.gpg

# Stable Channel:
sudo dnf config-manager --add-repo https://download.sublimetext.com/rpm/stable/x86_64/sublime-text.repo

# Install Sublime Text:
sudo dnf install -y sublime-text
```

1. Visual Studio Code:
    

```bash
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc

sudo sh -c 'echo -e "[code]\nname=Visual Studio Code\nbaseurl=https://packages.microsoft.com/yumrepos/vscode\nenabled=1\ngpgcheck=1\ngpgkey=https://packages.microsoft.com/keys/microsoft.asc" > /etc/yum.repos.d/vscode.repo'

sudo dnf check-update

sudo dnf install code
```

1. Gitignore # <mark>from the software center</mark>
    
2. GitHub Desktop # <mark>from software center</mark>
    
3. Telegram # <mark>from the software center</mark>
    
4. Spotify # <mark>from software center</mark>
    
5. Microsoft Edge # <mark>from the software cente</mark>r
    
6. Brave:
    

```bash
sudo dnf install dnf-plugins-core

sudo dnf config-manager --add-repo https://brave-browser-rpm-release.s3.brave.com/x86_64/

sudo rpm --import https://brave-browser-rpm-release.s3.brave.com/brave-core.asc

sudo dnf install brave-browser
```

1. Onlyoffice-Desktop Edition # <mark>from the software cente</mark>r
    
2. Whatsapp-Desktop # <mark>from the software cente</mark>r
    
3. OBS:
    

```bash
sudo dnf -y install obs-studio
```

1. Fonts:
    
    ```bash
    sudo dnf install -y fira-code-fonts 'mozilla-fira*' 'google-roboto*'
    ```
    

# Terminal Setup:

→Fish shell:-

Refer to:-

[https://mutschler.eu/linux/install-guides/fedora-post-install/](https://mutschler.eu/linux/install-guides/fedora-post-install/)

### ZSH shell Setup:

**Can Refer to:**

[https://www.youtube.com/watch?v=PZTLIVQxxEY](https://www.youtube.com/watch?v=PZTLIVQxxEY)

### **OR**

1. **Verify the** `shell` you are using:
    

```bash
echo $0
#Bash  (/usr/bash)
```

1. **Installing** `ZSH`:
    

```bash
sudo dnf install zsh
```

1. **Change** `shell`:
    

```bash
chsh
#Enter password

#input
/bin/zsh   # Login Shell
```

* Logout from the session OR reboot
    

```bash
#Reboot
sudo reboot now
```

1. `ZSH` initial setup:
    

```bash
#options
# (q) Quit and do nothing.
# (0) Exit, creating the file ~/.zshrc
# (1) Continue to the main menu
# (2) Populate your ~/.zshrc with the configuration recomended

# Input
q
```

* **Verify the** `shell` :
    

```bash
# input
echo $0

# output
zsh
```

* **Now install “**`Oh My ZSH!`”
    

> You can refer to the official website(*preferred*) :

[https://ohmyz.sh/](https://ohmyz.sh/)

OR

> Run this command:

**(Prerequisite :** `Git`**,** `Curl`**)**

```bash
# Install "Oh My ZSH!"
sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

* **Install** `PowerLevel10K` **Terminal theme** :
    
* Can Refer to:
    
    [https://github.com/romkatv/powerlevel10k](https://github.com/romkatv/powerlevel10k)
    
* click→ Installation
    
* click→ Oh My Zsh
    
* Then run the command:
    

```bash
git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k
```

* Get the Fonts:
    

```bash
#clone
git clone https://github.com/Priyansusahoo/Terminal_OH-MY-ZSH.git
```

> copy the files in powerline-fonts to ~/.fonts folder:

```bash
cd
mkdir ~/.fonts
cd Terminal_OH-MY-ZSH/powerline-fonts/
cp * /home/PS/.fonts
```

* Go to Gnome-Tweaks:
    

* Go to Fonts.
    
* Change the `Monospace Text = MesloLGS NF Regular`
    
* Save the changes
    
* Restart the terminal
    
    * Then change `ZSH_THEME` :
        

```bash
cd

sudo nano ~/.zshrc

#Edit
ZSH_THEME="powerlevel10k/powerlevel10k"
```

> **Then Configure as per your liking.**

If you guys have any suggestions, feel free to contact me on:

* **priyansusahoo1@gmail.com**
    
* [https://twitter.com/Priyansu2000](https://twitter.com/Priyansu2000)
    
* [https://www.linkedin.com/in/priyansu1/](https://www.linkedin.com/in/priyansu1/)