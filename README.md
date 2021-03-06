# kvm-stuff

### Ubuntu server guest install

```shell
export GUEST_NAME=controller-1; sudo virt-install \
--virt-type=kvm \
--name ${GUEST_NAME} \
--memory 2048 \
--vcpus=2 \
--os-variant=ubuntu16.04 \
--virt-type=kvm \
--hvm \
--location /home/diversario/os_images/ubuntu-17.04-server-amd64.iso \
--network=bridge=br0,model=virtio \
--graphics vnc,listen=0.0.0.0 \
--console pty,target_type=serial \
--disk pool=nuc-server-vg,size=10 \
--extra-args "console=ttyS0,115200n8 serial hostname=${GUEST_NAME}" \
--initrd-inject=/home/diversario/os_preseed/preseed.cfg
```

### Enable console

```shell
sudo systemctl enable serial-getty@ttyS0.service
sudo systemctl start serial-getty@ttyS0.service
```

### CSSH alternative
https://github.com/dennishafemann/tmux-cssh
