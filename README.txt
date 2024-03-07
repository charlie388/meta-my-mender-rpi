# This project is extract version from meta-mender-community
# https://github.com/mendersoftware/meta-mender-community
# https://hub.mender.io/t/raspberry-pi-3-model-b-b/57
# https://hub.mender.io/t/how-to-configure-networking-using-systemd-in-yocto-project/1097
# I tested this on rpi-3-b and rpi-3-b-plus

mkdir my-mender-rpi
cd my-mender-rpi
repo init -u git@github.com:charlie388/meta-my-mender-rpi.git -b kirkstone
repo sync
source setup-environment
# modify MENDER_DTB_NAME_FORCE and MENDER_SERVER_URL in conf/local.conf
# modify wifi 
wpa_passphrase "my ssid" "my psk" > ../sources/meta-my-mender-rpi/recipes-connectivity/wpa-supplicant/files/wpa_supplicant-nl80211-wlan0.conf

sed -i '/#psk=/d' ../sources/meta-my-mender-rpi/recipes-connectivity/wpa-supplicant/files/wpa_supplicant-nl80211-wlan0.conf

bitbake core-image-base

Note:
# how to install repo comd on ubuntu
# https://gerrit.googlesource.com/git-repo#install
# https://source.android.com/docs/setup/download#installing-repo
sudo apt-get install python-is-python3
mkdir -p ~/.bin
PATH="${HOME}/.bin:${PATH}"
curl https://storage.googleapis.com/git-repo-downloads/repo > ~/.bin/repo
chmod a+rx ~/.bin/repo
