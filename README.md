### Device specific configuration to turn your Raspberry Pi 4 or Raspberry Pi 5 into a Car Infotainment System (Android Automotive OS / AAOSP 16)

***

### **!! IMPORTANT:** This is pretty much still a **work-in-progress**! Probably not a great idea to use this yet. 

### How to build (Ubuntu 22.04 LTS):

1. Establish [Android build environment](https://source.android.com/docs/setup/start/requirements).

2. Install additional packages:

```
sudo apt-get install dosfstools e2fsprogs fdisk kpartx mtools rsync
```

3. Initialize repo:

```
repo init -u https://android.googlesource.com/platform/manifest -b android-16.0.0_r1 --depth=1
curl -o .repo/local_manifests/manifest_brcm_rpi.xml -L https://raw.githubusercontent.com/raspberry-vanilla/android_local_manifest/android-16.0/manifest_brcm_rpi.xml --create-dirs
curl -o .repo/local_manifests/remove_projects.xml -L https://raw.githubusercontent.com/raspberry-vanilla/android_local_manifest/android-16.0/remove_projects.xml
curl -o .repo/local_manifests/manifest_pi_car.xml -L https://raw.githubusercontent.com/raspberry-car-unit/android_local_manifest/master/manifest_pi_car.xml --create-dirs
```

4. Sync source code:

```
repo sync
```

5. Setup Android build environment:

```
. build/envsetup.sh
```

6. Select the device (`rpi4` or `rpi5`) and build target:

```
lunch aosp_rpi4_car-bp2a-userdebug
```
```
lunch aosp_rpi5_car-bp2a-userdebug
```
7. Compile:

```
make bootimage systemimage vendorimage -j$(nproc)
```

8. Make flashable image for the device (`rpi4` or `rpi5`):

```
./rpi4-mkimg.sh
```
```
./rpi5-mkimg.sh
```
