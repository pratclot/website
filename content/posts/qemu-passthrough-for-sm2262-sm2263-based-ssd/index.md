+++
title = 'Qemu Passthrough for Sm2262 Sm2263 Based Ssd'
date = 2022-11-02 11:38:56.297000
+++

{{< figure src="./images/Screenshot_from_2022_11_02_11_39_11_87acee04fb.png" alt="picture of the error in Gnome interface" class="center" >}}

I have an NVMe device that I use to passthrough to a virtual machine on Linux. It has some internal issue, a workaround that worked for me so far was described [here](https://bugzilla.kernel.org/show_bug.cgi?id=202055#c42):

```
<hostdev mode="subsystem" type="pci" managed="yes">
  <source>
    <address domain="0x0000" bus="0x6f" slot="0x00" function="0x0"/>
  </source>
  <boot order="1"/>
  <alias name="ua-sm2262"/>
  <address type="pci" domain="0x0000" bus="0x00" slot="0x07" function="0x0"/>
</hostdev>
```
```
  <qemu:commandline>
    <qemu:arg value="-set"/>
    <qemu:arg value="device.ua-sm2262.x-msix-relocation=bar2"/>
  </qemu:commandline>
```

Since some release of qemu it seems to no longer work and give an error message like this:

```
Error starting domain: internal error: process exited while connecting to monitor: qemu-system-x86_64: -set device.ua-sm2262.x-msix-relocation=bar2: there is no device "ua-sm2262" defined
```

Turns out the syntax has changed, and the solution is posted [here](https://bbs.archlinux.org/viewtopic.php?id=276409). Now I have it working with this:

```
  <qemu:override>
    <qemu:device alias="ua-sm2262">
      <qemu:frontend>
        <qemu:property name="x-msix-relocation" type="string" value="bar2"/>
      </qemu:frontend>
    </qemu:device>
  </qemu:override>
  ```