# Local Mac Environment Setup

### Single Step using wrapper script to bootstrap the setup process
Open Terminal and run the following command in a new directory/folder ( eg. mkdir insta; cd insta )

This project is to setup local Mac development environment with most of the required tools for running local builds and configs for applications using **Homebrew** [(http://brew.sh)](http://brew.sh/)  and **Ansible** [(www.ansible.com)](http://www.ansible.com/)

All instructions covered have been tested on Sierra

### Prerequisite:

Install git

Install XCode Command line tools

### `macsetup` repo Directory Structure:

```
├── README.md
├── ansible
│   └── playbooks
│       ├── app.yml
│       ├── build.yml
│       ├── ci.yml
│       ├── common.yml
│       ├── deploy.yml
│       ├── list.yml
│       ├── mac_pkgs.yml
│       ├── mysql.yml
│       ├── node.yml
│       ├── ql.yml
│       ├── remove.yml
│       ├── scala.yml
│       ├── site.yml
│       └── zsh.yml
└── setup.sh

```


   `site.yml` has below categories of tools, Each set of tools has separate `yml` file, based on the requirement uncomment the required *yml* files in `setup.yml`. By default *common.yml, build.yml, deploy.yml* are uncommented

 > **common.yml**  — Basic and gnu tools
 >
 > **app.yml**  ->   Installs applications (google-chrome, vlc, ..)
 >
 > **ci.yml**  ->   Installs CI tools (jenkins, sonar, artifactory)
 >
 > **node.yml**  ->   Installs npm and Node.js tools
 >
 > **ql.yml**  ->   Installs Quicklook plugins
 >
 > **scala.yml**  ->   Installs build tool for scala
 >
 >**build.yml**    —> tools required for running builds
 >
 >**deploy.yml**   —>  Virtualization/Deploy tools like docker and virtual box
 >
 > **list.yml**    - Lists all installed tools using brew

# How to Run

## Option 2: Using Git clone

 * Open Terminal and clone the git repo

 To install the tools we need macsetup git repo

    git clone git@github.com:bmaddali/macsetup.git

* Navigate to cloned macsetup directory run setup.sh (setup.sh will take's care of installing Brew, Ansible and the tools)

    ./setup.sh

## Option 3: To install a specific set of utilities

Run the following command to install required utilities (if you don't need all)

    ansible-playbook -i "localhost," -c local ansible/playbooks/<required>.yml

## Removing Installed tools

- in remove.yml — Uncomment the list of tools to uninstall and run below

    ansible-playbook -i "localhost," -c local ansible/playbooks/remove.yml


*Note: We should have at least one uncommented list item in each task otherwise Removal task will through error*


## Successful run looks like

```
vagrants-Mac:local_mac_setup vagrant$ ./setup.sh

PLAY [localhost] **************************************************************

GATHERING FACTS ***************************************************************
ok: [localhost]

PLAY [localhost] **************************************************************

TASK: [Install Homebrew taps] *************************************************
changed: [localhost] => (item=homebrew/dupes)
changed: [localhost] => (item=homebrew/versions)
changed: [localhost] => (item=homebrew/completions)
changed: [localhost] => (item=caskroom/cask)
changed: [localhost] => (item=caskroom/versions)

TASK: [Installing Homebrew-cask] **********************************************
changed: [localhost]

TASK: [Installing tools using Homebrew Cask] **********************************
changed: [localhost] => (item=iterm2)
changed: [localhost] => (item=java)
changed: [localhost] => (item=facter)
changed: [localhost] => (item=sublime-text3)

TASK: [Installing tools using Homebrew] ***************************************
changed: [localhost] => (item=coreutils)
changed: [localhost] => (item=ack)
changed: [localhost] => (item=bash)
changed: [localhost] => (item=binutils)
changed: [localhost] => (item=csshx)
changed: [localhost] => (item=diffutils)
changed: [localhost] => (item=git)
changed: [localhost] => (item=gnutls)
changed: [localhost] => (item=gzip)
changed: [localhost] => (item=less)
changed: [localhost] => (item=openssh)
changed: [localhost] => (item=rsync)
changed: [localhost] => (item=shellcheck)
changed: [localhost] => (item=ssh-copy-id)
changed: [localhost] => (item=subversion)
changed: [localhost] => (item=tree)
changed: [localhost] => (item=wdiff)
changed: [localhost] => (item=wget)
changed: [localhost] => (item=zsh)

TASK: [Installing tools using Homebrew with default names] ********************
changed: [localhost] => (item=findutils)
changed: [localhost] => (item=gnu-indent)
changed: [localhost] => (item=gnu-sed)
changed: [localhost] => (item=gnu-tar)
changed: [localhost] => (item=gnu-which)
changed: [localhost] => (item=grep)

PLAY [localhost] **************************************************************

TASK: [shell echo `brew list; brew cask list`] ********************************
changed: [localhost]

TASK: [Listing installed tools using Homebrew and Homebrew Cask] **************
ok: [localhost] => {
    "msg": "ack ansible autoconf axel bash binutils brew-cask coreutils diffutils docker docker-compose docker-machine docker-swarm findutils gdbm gettext git gmp gnu-indent gnu-sed gnu-tar gnu-which gnutls grep gzip jenv less libtasn1 libyaml maven maven-completion nettle openssh openssl pcre readline sqlite subversion tree unzip vagrant-completion wdiff wget zsh eclipse-jee facter iterm2 java java7 xa radar sublime-text3 vagrant virtualbox virtualbox-extension-pack"
}

PLAY RECAP ********************************************************************
localhost                  : ok=8    changed=2    unreachable=0    failed=0
```

Finding Homebrew Packages

http://macappstore.org
http://searchbrew.com
http://linuxbrew.sh

### dotfiles - Brewfile

    https://github.com/pstadler/dotfiles

### Fixed permission issues

    compaudit | xargs chmod g-w,o-w
