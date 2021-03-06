# Modified by JakeFrostyYT
```
to download packages and save it locally
just use a script i found
apt-get download $(apt-cache depends --recurse --no-recommends --no-suggests --no-conflicts --no-breaks --no-replaces --no-enhances <replace-this-with-package> | grep "^\w" | sort -u)

the main package we need is kali-linux-nethunter so just do
apt-get download $(apt-cache depends --recurse --no-recommends --no-suggests --no-conflicts --no-breaks --no-replaces --no-enhances kali-linux-nethunter:arm64 | grep "^\w" | sort -u)

Use the script only inside the repo/(build_arch) folder, for arm64 go to arm64 folder and use the script i provided, it will download the packages and dependencies recursively
```
# NetHunter chroot builder

Build a basic NetHunter chroot

## Docker support
```bash
docker build -t nethunter .
docker run --privileged --name nethunter_build -i -t nethunter 2>&1 | tee output.log
docker cp nethunter_build:/root/nethunter-fs/output .
```

## Dependencies

This could be built on any debian based system but I recommend building on Kali.

```bash
apt-get install -y git-core gnupg flex bison gperf libesd0-dev build-essential \
zip curl libncurses5-dev zlib1g-dev libncurses5-dev gcc-multilib g++-multilib \
parted kpartx debootstrap pixz qemu-user-static abootimg cgpt vboot-kernel-utils \
vboot-utils bc lzma lzop xz-utils automake autoconf m4 dosfstools rsync u-boot-tools \
schedtool git e2fsprogs device-tree-compiler ccache dos2unix debootstrap
```

## Running by itself

To create a full NetHunter system:
```bash
./build.sh -f
```
To create a minimal NetHunter filesystem:
```bash
./build.sh -m
```
