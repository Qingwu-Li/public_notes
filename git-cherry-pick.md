> ```
> git remote add kernelorg https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux.git
> git fetch kernelorg
> ```
>
> 

6 new patches in v5.9.15

>  » git log --oneline leica/5.4-2.1.x-imx/crocodile..v5.9.15 -- \
>  drivers/power/supply/bq27xxx_battery.c \
>  drivers/power/supply/bq27xxx_battery_hdq.c \
>  drivers/power/supply/bq27xxx_battery_i2c.c include/linux/power/bq27xxx_battery.h | tee /dev/null
>  
>  730c9df7b73b Krzysztof Kozlowski      6 weeks ago  power: supply: bq27xxx: report "not charging" on all types
>  707d678a5c7c Dan Murphy              5 months ago  power: supply: bq27xxx_battery: Add the BQ28z610 Battery monitor
>  6f24ff97e323 Dan Murphy              5 months ago  power: supply: bq27xxx_battery: Add the BQ27Z561 Battery monitor
>  81bd45fc36e3 Alexander A. Klimov     5 months ago  power: supply: bq2xxxx: Replace HTTP links with HTTPS ones
>  149ed3d404c9 Pali Rohár              8 months ago  change email address for Pali Rohár
>  583b53ece0b0 Dmitry Osipenko         9 months ago  power: supply: bq27xxx_battery: Silence deferred-probe error

2 of them are already part (backported) of crocodile branch

>  » git log --oneline v5.9.15..leica/5.4-2.1.x-imx/crocodile -- \
>  drivers/power/supply/bq27xxx_battery.c \
>  drivers/power/supply/bq27xxx_battery_hdq.c \
>  drivers/power/supply/bq27xxx_battery_i2c.c include/linux/power/bq27xxx_battery.h | tee /dev/null
>  
>  a10ed3b55fed Krzysztof Kozlowski      6 weeks ago  power: supply: bq27xxx: report "not charging" on all types
>  b7dee304aa0e Dmitry Osipenko         8 months ago  power: supply: bq27xxx_battery: Silence deferred-probe error

2 are not needed (email, URL staff)

> 81bd45fc36e3 Alexander A. Klimov     5 months ago  power: supply: bq2xxxx: Replace HTTP links with HTTPS ones
>  149ed3d404c9 Pali Rohár              8 months ago  change email address for Pali Rohár

2 are left

> 707d678a5c7c Dan Murphy              5 months ago  power: supply: bq27xxx_battery: Add the BQ28z610 Battery monitor
>  6f24ff97e323 Dan Murphy              5 months ago  power: supply: bq27xxx_battery: Add the BQ27Z561 Battery monitor

cherry-pick them one-by one, starting with the oldest one

>  » git cherry-pick --edit -s -x 6f24ff97e323
>   » git status -s

fix conflicts and commit

>  » vim drivers/power/supply/bq27xxx_battery.c
>   » git add drivers/power/supply/bq27xxx_battery.c
>   » git commit -s

same for the second patch

>  » git cherry-pick --edit -s -x 707d678a5c7c

no conflicts as we could see



[linux-5.9.y](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux.git/log/?h=linux-5.9.y)



git cherry-pick --abort



```
git cherry-pick [<options>] <commit-ish>...

常用options:
    --quit                退出当前的chery-pick序列
    --continue            继续当前的chery-pick序列
    --abort               取消当前的chery-pick序列，恢复当前分支
    -n, --no-commit       不自动提交
    -e, --edit            编辑提交信息
```



```
git log --oneline STMicr/linux-4.19.y-gh..leica/5.4-2.1.x-imx/crocodile -- drivers/iio/magnetometer | tee /dev/null
176fb9423ab8 iio:magnetometer:ak8975 Fix alignment and data leak issues.
ead750685280 iio: magnetometer: ak8974: Fix runtime PM imbalance on error
7cc8cad2bef9 iio:magnetometer:ak8974: Fix alignment and data leak issues
a79f53a2f5af iio: magnetometer: ak8974: Fix negative raw values in sysfs
e031d5f558f1 iio:st_sensors: remove buffer allocation at each buffer enable
9cd15d521a3a iio: remove get_irq_data_ready() function pointer and use IRQ number directly
6ee19af415c5 iio:magn: preenable/postenable/predisable fixup for ST magn buffer
3f2cde742632 iio: magnetometer: mmc35240: Fix a typo in the name of a constant
062809ef7733 iio: make st_sensors drivers use regmap
1ecd245e0eb2 iio: move 3-wire spi initialization to st_sensors_spi
291d83f2f4ef iio:magn: device settings are set immediately during probe
aa4e75c85076 iio:magn: introduce st_magn_get_settings() function
d2912cb15bdd treewide: Replace GPLv2 boilerplate/reference with SPDX - rule 500
a61127c21302 treewide: Replace GPLv2 boilerplate/reference with SPDX - rule 335
36edc93958e0 treewide: Replace GPLv2 boilerplate/reference with SPDX - rule 330
2025cf9e193d treewide: Replace GPLv2 boilerplate/reference with SPDX - rule 288
fda8d26e61fc treewide: Replace GPLv2 boilerplate/reference with SPDX - rule 177
c942fddf8793 treewide: Replace GPLv2 boilerplate/reference with SPDX - rule 157
16216333235a treewide: Replace GPLv2 boilerplate/reference with SPDX - rule 1
ec8f24b7faaf treewide: Add SPDX license identifier - Makefile/Kconfig
09c434b8a004 treewide: Add SPDX license identifier for more missed files
536cc27deade iio: hmc5843: fix potential NULL pointer dereferences
67b9d4d0985f iio: ak8975: improve code readability
8d7ea73814b4 iio: magnetometer: hmc5843: add mount matrix support
d9842c770a47 iio: magnetometer: bmc150: add mount matrix support
fb1589710efe iio: Allow to read mount matrix from ACPI
1dca9bdec6cb iio: magnetometer: mag3110: add vdd/vddio regulator operation support
c6cbcdea7ab9 Merge tag 'iio-for-4.21b' of git://git.kernel.org/pub/scm/linux/kernel/git/jic23/iio into staging-next
d5d12ce229c1 Merge 4.20-rc5 into staging-next
0a9ff2a13b46 iio: magnetometer: ak8975: Add the "AKM9911" ACPI HID
121354b2eceb iio: magnetometer: Add driver support for PNI RM3100
0145b50566e7 iio/hid-sensors: Fix IIO_CHAN_INFO_RAW returning wrong values for signed numbers
2eb4c9f2a5d7 iio:magnetometer: st_magn: add BDU settings
0d92aa2c272f iio:magnetometer: st_magn: add LSM9DS1 support
53759e259da4 iio: magnetometer: add clarifying comment
fe5192ac81ad iio:st_magn: Fix enable device after trigger
2019738cc8e3 iio: st_sensors: miscellaneous cleanup
f9c4c27f1be0 iio: magnetometer: hmc5843: Fixed a comment error.
liqiw@aherlnxbspsrv01:/development/bsp-user-workspaces/liqiw/Magnetometer/linux-leica$ git log --oneline leica/5.4-2.1.x-imx/crocodile..STMicr/linux-4.19.y-gh -- drivers/iio/magnetometer | tee /dev/null
df6b505c6979 drivers:iio: Added support to ST MEMS devices
dd106d198dee iio: hmc5843: fix potential NULL pointer dereferences
855f9dc87160 iio:st_magn: Fix enable device after trigger
ec800c8b028e iio/hid-sensors: Fix IIO_CHAN_INFO_RAW returning wrong values for signed numbers


```

   





```
git log --oneline STMicr/linux-4.19.y-gh..leica/5.4-2.1.x-imx/crocodile \
-> -- \drivers/iio/magnetometer/st_mag40_buffer.c \
> drivers/iio/magnetometer/st_mag40_core.c \
> drivers/iio/magnetometer/st_mag40_core.h \
> drivers/iio/magnetometer/st_mag40_i2c.c \
> drivers/iio/magnetometer/st_mag40_spi.c | tee /dev/null
liqiw@aherlnxbspsrv01:/development/bsp-user-workspaces/liqiw/Magnetometer/linux-leica$

 git log --oneline leica/5.4-2.1.x-imx/crocodile..STMicr/linux-4.19.y-gh \
>  -- \drivers/iio/magnetometer/st_mag40_buffer.c \
> drivers/iio/magnetometer/st_mag40_core.c \
> drivers/iio/magnetometer/st_mag40_core.h \
> drivers/iio/magnetometer/st_mag40_i2c.c \
> drivers/iio/magnetometer/st_mag40_spi.c | tee /dev/null
df6b505c6979 drivers:iio: Added support to ST MEMS devices


git cherry-pick --edit -s -x df6b505c6979



```







```
git log --oneline leica/5.4-2.1.x-imx/crocodile.. kernelorg/master -- drivers/power/supply/bq27xxx_battery.c drivers/power/supply/bq27xxx_battery_hdq.c drivers/power/supply/bq27xxx_battery_i2c.c include/linux/power/bq27xxx_battery.h | tee /dev/null
```



```
xx_battery_hdq.c drivers/power/supply/bq27xxx_battery_i2c.c include/linux/power/bq27xxx_battery.h | tee /dev/null
38525c6919e2 Merge tag 'for-v5.10' of git://git.kernel.org/pub/scm/linux/kernel/git/sre/linux-power-supply
6925478cad27 power: supply: Constify static w1_family_ops structs
41a7431dbaa3 power: supply: bq27xxx: add support for TI bq34z100
7be64ae0bf36 power: supply: bq27xxx: add separate flag for capacity inaccurate
c02ca2019866 power: supply: bq27xxx: add separate flag for single SoC register
bffa569fc985 power: supply: bq27xxx: adjust whitespace and use BIT() for bitflags
7bf738ba1107 power: supply: bq27xxx: report "not charging" on all types
44ff56c022c0 power: bq27xxx: Update to SPDX licensing
4024810c5aad power: supply: bq27xxx: Simplify with dev_err_probe()
707d678a5c7c power: supply: bq27xxx_battery: Add the BQ28z610 Battery monitor
6f24ff97e323 power: supply: bq27xxx_battery: Add the BQ27Z561 Battery monitor
81bd45fc36e3 power: supply: bq2xxxx: Replace HTTP links with HTTPS ones
149ed3d404c9 change email address for Pali Rohár
583b53ece0b0 power: supply: bq27xxx_battery: Silence deferred-probe error
```

```


git log --oneline kernelorg/master..leica/5.4-2.1.x-imx/crocodile  -- drivers/power/supply/bq27xxx_battery.c drivers/power/supply/bq27xxx_battery_hdq.c drivers/power/supply/bq27xxx_battery_i2c.c include/linux/power/bq27xxx_battery.h | tee /dev/null
```

```
a10ed3b55fed power: supply: bq27xxx: report "not charging" on all types
b7dee304aa0e power: supply: bq27xxx_battery: Silence deferred-probe error
```

```


git log --oneline leica/5.4-2.1.x-imx/crocodile.. v5.9.15 -- drivers/power/supply/bq27xxx_battery.c drivers/power/supply/bq27xxx_battery_hdq.c drivers/power/supply/bq27xxx_battery_i2c.c include/linux/power/bq27xxx_battery.h | tee /dev/null
```



git log --oneline kernelorg/master..power_supply_master  -- drivers/power/supply/bq27xxx_battery.c drivers/power/supply/bq27xxx_battery_hdq.c drivers/power/supply/bq27xxx_battery_i2c.c include/linux/power/bq27xxx_battery.h | tee /dev/null



git log --oneline kernelorg/master..kernelorg/power_supply_master  -- drivers/power/supply/bq27xxx_battery.c drivers/power/supply/bq27xxx_battery_hdq.c drivers/power/supply/bq27xxx_battery_i2c.c include/linux/power/bq27xxx_battery.h | tee /dev/null



/data2/liqiw/geosurv/build-output/work-shared/crocodile/kernel-source/include/linux/device.h



git log --oneline power_supply_master.. kernelorg/master -- drivers/power/supply/bq27xxx_battery.c drivers/power/supply/bq27xxx_battery_hdq.c drivers/power/supply/bq27xxx_battery_i2c.c include/linux/power/bq27xxx_battery.h include/linux/device.h | tee /dev/null





git log --oneline kernelorg/master.. power_supply_master -- drivers/power/supply/bq27xxx_battery.c drivers/power/supply/bq27xxx_battery_hdq.c drivers/power/supply/bq27xxx_battery_i2c.c include/linux/power/bq27xxx_battery.h include/linux/device.h | tee /dev/null