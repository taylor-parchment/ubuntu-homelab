These troubleshooting logs will include issues encountered while setting up my server and its services, along with steps taken to diagnose and resolve them.

Issue|Cause|Resolution|Notes
-----|-----|----------|-----
Running `docker compose up` returns error "permission denied while trying to connect to the docker API at unix:///var/run/docker.sock".|The user (the only current user of the system, me) was not a member of the `docker` group, and did not have permission to access the Docker socket.|Added my user to the `docker` group with the `sudomod` command and verified with `groups` after relogging. Successfully started a Docker container with the correct permission.|Linux group membership controls a lot of system resources. You can always verify group membership with the `groups` command.

Issue|Cause|Resolution|Notes
-----|-----|----------|-----
Network services became unreachable after closing the laptop lid, even though the system continued running.|Common causes would be lid switch settings or Wifi power manager.|I tried modifying the systemd lid switch settings, but the issue persisted after disabling all sleep on lid closed settings. This could be a hardware issue. Since the Surface Pro has a detachable keyboard and all troubleshooting is done via SSH, the keyboard can simply remain detached.|Hardware specific behavior can be an issue...

Issue|Cause|Resolution|Notes
-----|-----|----------|-----
My external hard drive was formatted as exFAT, which isn't optimal for Linux, and contained an unnecessary partition.|The HDD is being repurposed.|Deleted the existing partitions and created a single Linux partition with `fdisk`. Formatted the partition as ext4 with `mkfs`. Configured automatic mounting with `/etc/fstab`.|`/etc/fstab` contains a lot of important mounting points, even the main OS drive! You have to be very careful modifying these files.
