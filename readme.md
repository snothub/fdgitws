```
_____________________________________
( Chuck Norris doesn't go hunting.... )
( CHUCK NORRIS GOES KILLING.          )
 -------------------------------------
        o   ^__^
         o  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||
                
```

 Git

``` bash
# merk: det finnes tre nivåer av git konfigurasjon: system (<git path>/etc/config), global (%USERPROFILE%/.gitconfig) og local konfigurasjon (<repo mappe>/.git/config). 
# Git ser etter konfigurasjon i den rekkefølgen, dvs local kan overstyre de andre, global kan overstyre system.
# det er som regel mest hensysnmessig for en bruker å legge inn ønsket konfigurasjon i global

# vise git konfigurasjon og hvor den er lagret
git config --list --show-origin

# åpne global konfig for redigering
git config --global -e

# alias seksjon i config
[alias]
	s = status
	l = log -10 --oneline
	dt = "!f() { git checkout \"$1\"; }; f"

# legge til nye alias
git config --global alias.last 'log -1 HEAD'
git config --global alias.visual '!gitk'
# ...vil ende opp slik
[alias]
	s = status
	l = log -10 --oneline
	dt = "!f() { git checkout \"$1\"; }; f"
	last = log -1 HEAD
	visual = '!gitk'

```

WSL2

#### Det meste jeg gjorde er beskrevet her med linker til relevante sider
https://johnbwoodruff.com/posts/more-epic-environment-wsl2/


``` powershell
# kjørt på forhånd, krever restart
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
wsl --set-default-version 2

```
Gå til Microsoft Store, søk på 'ubuntu' og installer derfra. Ny terminal kommer opp. Lag brukernavn og passord for å fullføre.

``` bash
cd /home # gå til hjemmeområde
sudo mkdir dev # lag en katalog for 
sudo chmod a=rwx dev # gjør mappen skrivbar og lesbar uten admin/sudo

sudo apt update && sudo apt install git # 

git config --global credential.https://dev.azure.com.useHttpPath true # nødvendig Git Credential Manager, bruker du SSH (se neste linje) er dette irrelevant

# generer SSH private/public key for den kontoen du ønsker å bruke, trykk Enter for å bruke foreslåtte verdier (anbefalt)
ssh-keygen -t rsa -b 4096 -C "user@domain.com" 
# kopier public key for å legge inn i Azure
cat ~/.ssh/id_rsa.pub
# gå til dev.azure.com, User settings og velg SSH public keys. Trykk New Key og legg inn navn og lim inn public SSH

# installer ZSH og OhMyZSH - https://github.com/ohmyzsh/ohmyzsh
sudo apt install zsh
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"


sudo apt install gedit # tekstredigering

exec zsh # kjør hver gang noe endres i config

```

> Legg også merke til at med OgMyZsh trenger du ikke lenger skrive "cd <mappe>", 
> men kan bare skrive mappenavn og <Enter> for å gå inn i mappen.
> Tilsvarende kan du skrive .. og <Enter> for å gå ut, og hver ekstra "." tar deg bakover i mappene, nice! :)

---

``` powershell

# powerlevel10k Theme:
git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k

# autosuggestions:
git clone --depth=1 https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions

gedit ~/.zshrc
# set ZSH_THEME="powerlevel10k/powerlevel10k"
# set plugins=(git docker dotnet z zsh-autosuggestions)

# Optional Chuck Norris plugin:
#  sudo apt install cowsay && sudo apt install fortune
# gedit ~/.zshrc
# set plugins=(... chucknorris)

```
