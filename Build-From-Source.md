```
mkdir -p ~/bin
sudo apt install curl

curl https://storage.googleapis.com/git-repo-downloads/repo >  ~/bin/repo
chmod a+x ~/bin/repo
export PATH=~/bin:$PATH

sudo apt-get update
sudo apt-get install -y openjdk-8-jdk git ccache automake \
      lzop bison gperf build-essential zip curl \
      zlib1g-dev g++-multilib python-networkx \
      libxml2-utils bzip2 libbz2-dev libbz2-1.0 \
      libghc-bzlib-dev squashfs-tools pngcrush \
      schedtool dpkg-dev liblz4-tool make optipng maven \
      libssl-dev bc bsdmainutils gettext python-mako \
      libelf-dev sbsigntool dosfstools mtools efitools \
      python-pystache git-lfs python3 flex

sudo apt-get install -y apt-transport-https ca-certificates curl
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
sudo apt-get update
sudo apt-get install -y docker-ce docker-ce-cli containerd.io
sudo usermod -aG docker $USER

git config --global user.email "you@example.com"
git config --global user.name "Your Name"
```
Build VM
```
mkdir ~/civ
cd ~/civ
repo init -u https://github.com/projectceladon/manifest.git -m stable-build/CIV_01.20.01.12_A10.xml
repo sync -c --quiet

#On Multiple builds
#make clobber

source build/envsetup.sh
lunch caas-userdebug
make SPARSE_IMG=true flashfiles -j $(nproc)
```

Build Container
```
mkdir ~/cic
cd ~/cic
repo init -u https://github.com/projectceladon/manifest -b celadon/p/mr0/master -m stable-build/CIC_01.20.01.12_A09.xml
repo sync -c --quiet

#make clobber
source build/envsetup.sh
lunch cic-userdebug
make cic -j $(nproc)
```
