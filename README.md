## Fedora Workstation Kickstart File

### Overview

Part of an overall project to adopt the "cattle" approach to my personal computing.

Designed to:

* Deploy Fedora (tested on F23) with a repeatable and automated method.
* Provide a single source of truth for the software I like to use.
* Encapsulate any optimisations/tricks I like to apply.

### Requirements
* This README assumes installation to a device with:
  * An internet connected ethernet port.
  * At least 15GB of HDD.
  * A webserver to host this kickstart file once it is configured.
* For machines with no eth port, use `livecd-iso-to-disk` then add the ks file to the USB.
  * https://github.com/rhinstaller/livecd-tools/blob/master/tools/livecd-iso-to-disk.sh

### Use
* Clone and enter this repository with:
  * `git clone http://github.com/sinner-/kickstart-fedora-workstation`.
  * `cd kickstart-fedora-workstation`.
* Configure the LUKS full disk encryption passphrase:
  * `sed -i 's/fdepassphrase/YOUR_FULL_DISK_ENCRYPTION_PASSPHRASE/' workstation.ks`.
* Configure the builtin users password:
  * `sed -i 's/userpassword/YOUR_USER_PASSWORD/' workstation.ks`.
* If you're not me you will probably also want to run:
  * `sed -i 's/sina/YOUR_NAME/' workstation.ks`.
* I configure the hostname to be "sina-laptop", if you want something else:
  * `sed -i 's/sina-laptop/YOUR_DESIRED_HOSTNAME/' workstation.ks`.
* Upload the kickstart file to your webserver. I normally use another local linux machine:
  * `python -m SimpleHTTPServer` (starts on port 8000).
* Boot Fedora Workstation netinst on the target install machine.
* At the boot screen, press UP to select the "install without verify" option and then TAB.
* Append the kickstart directive to the end of the boot string:
  * `inst.ks=http://<WEB_SERVER_IP>:<PORT>/fedora-desktop.ks`
* Hit ENTER. Install will begin and complete without any further prompt.
