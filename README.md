# zigbee2mqtt
This repo is a placeholder to store nodes_modules dependencies for gentoo ebuild app-misc/zigbee2mqtt

## How to create anew zigbee2mqtt version

### Create a temporary ebuild for new version a.b.c
Enter your repo and copy last version x.y.z ebuild to the new version :
```bash
cd /var/db/repos/xxx/app-misc/zigbee2mqtt
cp zigbee2mqtt-x.y.z.ebuild zigbee2mqtt-a.b.c.ebuild
```

Now edit new ebuild and comment nodes_modules.tar.xz part in SRC_URI (line 13)
Unpack the source :
```bash
ebuild zigbee2mqtt-a.b.c.ebuild digest clean unpack
```

Go in the extracted source, generate nodes_modules :
```bash
pushd /var/tmp/portage/app-misc/zigbee2mqtt-a.b.c/work/zigbee2mqtt-a.b.c
npm install
```
Generate nodes_module-a.b.c.tar.xz
```bash
pushd ..
XZ_OPT=-9 tar -Jcvf zigbee2mqtt-a.b.c-nodes_modules.tar.xz zigbee2mqtt-a.b.c/node_modules/
```

Upload node_modules in a release tagged a.b.c
