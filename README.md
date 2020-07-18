# Element: decentralized, encrypted chat & collaboration

_.&nbsp;.&nbsp;.&nbsp;packaged for Fedora and OpenSUSE_

_**What is Element?**_ Decentralised, encrypted chat & collaboration powered by [matrix].

_**What is Matrix?**_ An open network for secure, decentralized communication.

In short, Element is an open-source, decentralized, end-to-end encrypted, team collaboration platform who's often compared to IRC, Rocket Chat, Mattermost, Slack, and Discord.

> Element was once branded Riot. The name changed as of version 1.7.0 (July, 2020).

More fully, Element is a desktop application implementing the client-side of the matrix protocol enabling decentralized, secure messaging for collaborative groups. This repository enables Element to be easily installed and maintained on the Fedora, Red Hat(IBM), and OpenSUSE family of Linux operating systems and tracks the source surrounding those builds. This GitHub repository maintains source RPM packages and spec files so you can rebuild Element if you are so inclined, though pre-built binaries have been conveniently built for you. See below for how to install and run Element on your Linux desktop.

All `*.src.rpm` packages provided in this GitHub repository are signed with [my GPG key](https://keybase.io/toddwarner/key.asc)<br />All binary RPMs are signed with the [Fedora Project's](https://fedoraproject.org/) [COPR GPG signing key](https://copr-be.cloud.fedoraproject.org/results/taw/element/pubkey.gpg)

> Please note that packages also exist for Android, Apple products, and Microsoft Windows. Element for the web (Chromebook and anyone) is available here: <https://app.element.io/> — slick!

#### More about&nbsp;.&nbsp;.&nbsp;.

* Element: <https://element.im/> and the source repositories, [riot-desktop](https://github.com/vector-im/riot-desktop) and [riot-web](https://github.com/vector-im/riot-web)
* Matrix: <https://matrix.org/> and <https://en.wikipedia.org/wiki/Matrix_(communication_protocol)>
* A couple reviews from [some dude](http://www.1500wordmtu.com/2016/slack-no-more-why-you-should-use-riotim-and-matrixorg), [TechCrunch](https://techcrunch.com/2016/09/19/riot-wants-to-be-like-slack-but-with-the-flexibility-of-an-underlying-open-source-platform/), and the [Slant community](https://www.slant.co/options/12764/~matrix-review)<br />_Unsurprisingly, I personally think Element is superior to Slack and Rocket Chat._

# tl;dr&nbsp;.&nbsp;.&nbsp;.

## I just want to install Element!

It's easy to install, run, and maintain Element. Current builds are provided for these platforms (x86\_64 only)&nbsp;.&nbsp;.&nbsp;.  
_Note: I will stop building for any version of an OS that is itself no longer supported_

Successful builds:
* **Fedora:** versions 31+
* **OpenSUSE:** Tumbleweed and Leap 15.2 as of Element 1.7.1
* **Flatpak:** Though I personally view Flatpaks as last resort packaging solutions (it is a brute force, relatively inefficient, but more secure! method of packaging), they do serve their purpose. **Leap 15.1, 15.2, and EL8(RHEL/CentOS) folks can use the Element-team supplied Flatpak:** <https://flathub.org/apps/details/im.riot.Riot>

Unsucessful builds:
* **CentOS (and RHEL):**
  - Last successful build version: Riot 1.5.
  - See also GitHub issues [#31](https://github.com/taw00/riot-rpm/issues/31) and [#33](https://github.com/taw00/riot-rpm/issues/33). See "Flatpak" below.
* **OpenSUSE:**
  - Leap 15.1: Riot 1.5 and older only. See also GitHub issue [#32](https://github.com/taw00/riot-rpm/issues/32). Install "Flatpak" instead, see below.

### [Fedora]

**Prep&nbsp;.&nbsp;.&nbsp;.**
```bash
# Should only need to do this prep phase once
# Configure the COPR repository
sudo dnf copr enable taw/element
# Install Fedora's distribution GPG keys
sudo dnf install -y distribution-gpg-keys
```
.&nbsp;.&nbsp;.&nbsp;alternative&nbsp;.&nbsp;.&nbsp;.
```bash
# Should only need to do this prep phase once
# Install GPG keys
sudo rpm --import https://keybase.io/toddwarner/key.asc
sudo rpm --import https://copr-be.cloud.fedoraproject.org/results/taw/element/pubkey.gpg
# Configure and enable the Element repository
sudo dnf install https://download.copr.fedorainfracloud.org/results/taw/element/fedora-32-x86_64/01558173-toddpkgs-element-repo/toddpkgs-element-repo-1.7-1.fc32.taw.noarch.rpm
```

**Install&nbsp;.&nbsp;.&nbsp;.**
```bash
# Install Element
sudo dnf install -y element --refresh
```

### [OpenSUSE]

**Prep (Leap 15.2)&nbsp;.&nbsp;.&nbsp;.**
```bash
# Should only need to do this prep phase once
# Install GPG keys
sudo rpm --import https://keybase.io/toddwarner/key.asc
sudo rpm --import https://copr-be.cloud.fedoraproject.org/results/taw/element/pubkey.gpg
# Configure and enable the Element repository
sudo zypper install https://download.copr.fedorainfracloud.org/results/taw/element/opensuse-leap-15.2-x86_64/01558173-toddpkgs-element-repo/toddpkgs-element-repo-1.7-1.suse.lp152.taw.noarch.rpm
sudo zypper modifyrepo -er "element-stable"
```

**Prep (Tumbleweed)&nbsp;.&nbsp;.&nbsp;.**
```bash
# Should only need to do this prep phase once
# Install GPG keys
sudo rpm --import https://keybase.io/toddwarner/key.asc
sudo rpm --import https://copr-be.cloud.fedoraproject.org/results/taw/element/pubkey.gpg
# Configure and enable the Element repository
sudo zypper install https://download.copr.fedorainfracloud.org/results/taw/element/opensuse-tumbleweed-x86_64/01558173-toddpkgs-element-repo/toddpkgs-element-repo-1.7-1.suse.tw.taw.noarch.rpm
sudo zypper modifyrepo -er "element-stable"
```

**Install&nbsp;.&nbsp;.&nbsp;.**
```bash
# Clean out the cache in case the change didn't get picked up
sudo zypper refresh
# Install element
sudo zypper install element
```

## I installed it, now I want to run Element!

Search for and select "Element" from your desktop or run `element` from the command line.

Note: If none of this made sense or you couldn't get it to work, Element can also be run as directly from your browser at <https://element.im/app>

## I installed it, now I want to ensure I get future updates!

Once you have followed the repository and installation instructions above, you should be notified of any future updates enabling you to update the software automatically. And you can always force a check with...

Note that with updates you may have to do a `killall element-desktop`). Quiting the application doesn't really "quit it" nor does the flush cache reload function in the UI.

```bash
# Fedora . . .
sudo dnf upgrade
```

```bash
# OpenSUSE . . .
sudo zypper update
```

I do this as a hobby, but I will try to be timely with my updates.

<!--
## I live on the edge! Do you have test packages available?

Yes!

1. Follow the steps described above to install the repository configure file.  
   _You will have to refresh it if you have done this before today._
2. Disable the stable repository and enable the testing repository...
```
# Fedora and RHEL/CentOS only
sudo dnf config-manager - - set-disabled element-stable
sudo dnf config-manager - - set-enabled riot-testing
sudo dnf list - - refresh |grep element
```
-->


# Disclaimer

I built these for my own use. I offer these builds for your own convenience. If it 'splodes your computer, I am sorry, but buyer beware. :) I am in no way affiliated with the originators of Element—[New Vector Ltd/Element](https://element.im/)—but I do thank them for their wonderful application and the community appreciates their welcoming approach to contributors like myself.

# Questions or comments&nbsp;.&nbsp;.&nbsp;.

Contact: **t0dd_at_protonmail.com** or find me at **@t0dd:matrix.org** after you have installed Element!
