# CMPE283-assignment-2 - Harsh Vaghasiya (016053102) , Rushabh Sheta (016038646)

## Team Members:
1) Harsh Vaghasiya - 016053102
2) Rushbha Sheta - 016038646

## Questions and Answers:
1) For each member in your team, provide 1 paragraph detailing what parts of the lab that member implemented / researched. (You may skip this question if you are doing the lab by yourself). <br><br>
**Answer:** <br><br>
----------------------
2) Describe in detail the steps you used to complete the assignment. Consider your reader to be someone skilled in software development but otherwise unfamiliar with the assignment. Good answers to this question will be recipes that someone can follow to reproduce your development steps. <br>
**Note:** I may decide to follow these instructions for random assignments, so you should make sure they are accurate. <br><br>
**Answer:**<br><br>
**Step-1: Created project in GCP.** <br><br>

**Step-2: Enabled Compute Engine API in order to create VM instance. Opened Google Cloud Shell and created VM instance with enabled nested virtualization in this project.** <br><br>

**To create VM instance with enabled nested virtualization, use following command:**<br>
**Note:** DON'T FORGET to make changes for project specific details in the following commmand such as project name, project id, zone details etc.<br>
>*gcloud beta compute instances create instance-1 --project=cmpe283l2 --zone=us-central1-a --machine-type=n2-standard-8 --network-interface=network-tier=PREMIUM,subnet=default --maintenance-policy=MIGRATE --provisioning-model=STANDARD --service-account=368584009094-compute@developer.gserviceaccount.com --scopes=https://www.googleapis.com/auth/cloud-platform --min-cpu-platform=Intel\ Cascade\ Lake --enable-display-device --create-disk=auto-delete=yes,boot=yes,device-name=instance-1,image=projects/ubuntu-os-cloud/global/images/ubuntu-2204-jammy-v20221201,mode=rw,size=100,type=projects/cmpe283l2/zones/us-central1-a/diskTypes/pd-ssd --no-shielded-secure-boot --shielded-vtpm --shielded-integrity-monitoring --reservation-affinity=any --enable-nested-virtualization --threads-per-core=2 --visible-core-count=4*

**Step-3: Logged into the VM instance using SSH.** <br><br>

**Step-4: Install Git. And Clone the kernel repository. Verify the contents of Linux Folder.** <br><br>
>*sudo apt-get install git*<br>
>*git --version*<br>
>*git clone https://github.com/harshv72/linux.git*<br>
>*cd linux*<br>
>*ls*<br>
>*git status*<br>
>*git remote -v*<br>

**Step-5: Run following commands to install dependencies.** <br><br>
>*sudo bash*<br>
>*apt-get update*<br>
>*apt install gcc make*<br>
>*apt-get install libncurses-dev gawk flex bison openssl libssl-dev dkms libelf-dev libudev-dev libpci-dev libiberty-dev autoconf*<br>

**Step-6: Run "uname -r" command to check the version of current kernel. Copy the config file. Run "make oldconfig" to read the existing .config file that was used for an old kernel. Edit .config file and make chages as shown in the screenshots below.**<br><br>
>*uname -r*<br>
>*cp -v /boot/config-$(uname -r) .config*<br>
>*make oldconifg*<br>

- Changes in .config file

**Step-7: Run following command to build the kernel for the first time. Run "sudo reboot" command to reboot VM instance. Run "uname -r" command again to check the version of updated kernel.**<br><br>
>*make -j 8 modules && make -j 8 && sudo make modules_install && sudo make install*<br>
>*sudo reboot*<br>
>*uname -r*<br>

**Step-8: cpuid.c file is located at : "/linux/arch/x86/kvm/" folder. And vmx.c file is located at:  "/linux/arch/x86/kvm/vmx/" folder. Make changes to these files as shown below""**<br><br>
- Changes for cpuid.c file:

- Changes for vmx.c file:

**Step-8: Run following command to build the kernel again for the second time.**<br><br>
>*make -j 8 modules && make -j 8 && sudo make modules_install && sudo make install*<br>

## Testing:

**Step-9: To install some basic GUI functionailities on our VM for inner-vm interaction, run following commands:**<br><br>
>*sudo apt update*<br>
>*sudo apt install*<br>
>*sudo apt update*<br>
>*sudo apt install --assume-yes wget tasksel*<br>
>*wget https://dl.google.com/linux/direct/chrome-remote-desktop_current_amd64.deb*<br>
>*sudo apt-get install --assume-yes ./chrome-remote-desktop_current_amd64.deb*<br>
>*sudo tasksel install ubuntu-desktop*<br>
>*sudo bash -c ‘echo “exec /etc/X11/Xsession /usr/bin/gnome-session” > /etc/chrome-remote-desktop-session’*<br>
>*sudo apt-get install xbase-clients*<br>

**Step-10: Run  following commands.**<br><br>
>*sudo systemctl status chrome-remote-desktop@$USER*<br>
>*sudo apt-get install qemu-kvm libvirt-daemon-system libvirt-clients bridge-utils*<br>
>*sudo lsmod | grep kvm*<br>
>*sudo rmmod kvm_intel*<br>
>*sudo rmmod kvm*<br>
>*sudo modprobe kvm*<br>
>*sudo modprobe kvm_intel*<br>
>*sudo lsmod | grep kvm*<br>
>*sudo adduser 'harshhimmatbhai_vaghasiya' libvirt*<br>
>*sudo getent group | grep libvirt*<br>
>*sudo adduser 'harshhimmatbhai_vaghasiya' kvm*<br>
>*sudo getent group | grep kvm*<br>
>*sudo virsh list --all*<br>
>*sudo systemctl status libvirtd*<br>
>*sudo systemctl enable --now libvirtd*<br>

**Step-11: Run code for Debian Linux Computer Setup. Install virt manager. Download and move .iso file to install ubuntu.**<br><br>
>*DISPLAY= /opt/google/chrome-remote-desktop/start-host --code="4/0AfgeXvvXzQRHUn9v7KUz4mxbZCve77kb55VNr3dq1yuMYOpnY-R83XLZusZGxeFclospJw" --redirect-url="https://remotedesktop.google.com/_/oauthredirect" --name=$(hostname)*<br>
>*sudo apt install virt-manager*<br>
>*wget https://releases.ubuntu.com/jammy/ubuntu-22.04.1-desktop-amd64.iso*<br>
>*sudo  mv ~/ubuntu-22.04.1-desktop-amd64.iso /var/lib/libvirt/images/*<br>

**Step-12: Install Ubuntu in remote desktop.**<br><br>

**Step-13: Update package installer. Install build-essential and cpuid package.**<br><br>
>*sudo apt-get update*<br>
>*sudo apt-get install*<br>
>*sudo apt-get install build-essential*<br>
>*sudo apt-get install -y cpuid*<br>

**Step-14: Create, compile and run the test file.**<br><br>
>*gedit test.c*<br>
>*gcc test.c*<br>
>*./a.out*<br>
