# Vivaldi_ARM
Vivaldi for arm based SBCs in one place


First download the Chromium patched FFMpeg to play H.264, e.g.

  wget https://launchpadlibrarian.net/435404265/chromium-codecs-ffmpeg-extra_76.0.3809.87-0ubuntu0.16.04.1_armhf.deb
  dpkg -i chromium-codecs-ffmpeg-extra_76.0.3809.87-0ubuntu0.16.04.1_armhf.deb

To install the contents of these files on an ARMhf device, copy the tar archive over to the target machine and issue the following:

  sudo tar Cfx / $ARCHIVE_NAME

After install of these libraries, open a terminal windows and issue the following commands and restart Vivaldi:

  mkdir -p ~/.config/vivaldi/WidevineCdm
  echo '{"Path":"/opt/WidevineCdm"}' > ~/.config/vivaldi/WidevineCdm/latest-component-updated-widevine-cdm

The Vivaldi 3.7 is pointing to /opt/google/chrome/WidevineCdm, but the script puts the files into /opt/WidevineCdm.

    Fixed broken links by opening a terminal windows and issuei ng the following commands: 

    cd /opt/vivaldi
    sudo rm WidevineCdm
    sudo ln -s /opt/WidevineCdm WidevineCdm

    After restart Vivaldi should show in vivaldi://components

    Widevine Content Decryption Module - Version: 4.10.1679.0
    Status - Up-to-date

    Change user agent with extension https://chrome.google.com/webstore/detail/user-agent-switcher/kchfmpdcejfkipopnolndinkeoipnoia Extension provided by Google didn't work as Cicorione mentioned above.

    Checked user agent from Chromium Mozilla/5.0 (X11; CrOS armv7l 13597.84.0) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/88.0.4324.187 Safari/537.36
    Instructions for User-agent settings: https://help.vivaldi.com/desktop/install-update/raspberry-pi/#netflix

Chromium

    The Widewine files work also with Chromium, and the Netflix videos seem to run smoother (better hardware acceleration?). 

    cd /usr/lib/chromium-browser
    sudo ln -s /opt/WidevineCdm WidevineCdm

    Once this is done you can test. The best bet for testing is to load 
    https://bitmovin.com/demos/drm (check if widevine is marked as enabled)
    
    Then try and load the examples marked DRM on 
    https://demo.castlabs.com


Raspberry Pi (general)
    
    For smoother playback we recommend to increase swap space. 
    Open a Terminal window and use the following command to change the SWAP from 100MB to change it to 2048MB:
    
    echo CONF_SWAPSIZE=2048 | sudo tee -a /etc/dphys-swapfile
    
    Then restart the swap service to apply the changes:    
    
    sudo /etc/init.d/dphys-swapfile stop
    sudo /etc/init.d/dphys-swapfile start 

Raspberry Pi 3

    Stopping the “hiss” when using analog out 
    Open a Terminal window and use the following commands:
    
    echo audio_pwm_mode=2 | sudo tee -a /boot/config.txt
    sudo reboot
