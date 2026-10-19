# Create Minimal Image from Buildroot
Build buildroot image
```bash
$ curl -L -O https://buildroot.org/downloads/buildroot-2023.02.7.tar.gz
$ tar zxvf buildroot-2023.02.7.tar.gz
$ cd buildroot-2023.02.7/
```

```bash
$ make menuconfig
$ make
```

```bash
$ cat output/images/rootfs.tar | docker import - buildroot
```

# Reuse image
```bash
$ cat << 'EOF' > Dockerfile
FROM buildroot
CMD ["echo", "Hello world!"]
EOF
$ docker build -t buildroot-hello-world .
$ docker run buildroot-hello-world
Hello world!
```
