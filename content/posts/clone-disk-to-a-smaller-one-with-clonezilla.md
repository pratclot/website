+++
title = 'Clone Disk to a Smaller One With Clonezilla'
date = 2022-12-04 22:47:35.600000
draft = false
+++
{{< figure src="/images/clone-disk-to-a-smaller-one-with-clonezilla/Screenshot_from_2022_12_04_23_06_57_d03e3ffaa3.png" alt="clonezilla image" class="center" >}}

Clonezilla allows to skip target disk size, and also has an option to create partitions on a new disk proportionally to the old ones.

In my case there was an HDD with 6 partitions and Windows 10, total size - 500 GB. The last three were C:, D: and the recovery image.

New SSD was only 240 GB, but as it turned out the partition backup made by Clonezilla took less than 200 GB.

For some reason, it was not possible to create partitions automatically - the creation of the last one would always get out of boundary and fail everything.

A comment [here](https://superuser.com/a/1361409) hints that you can tell Clonezilla to skip partition creation altogether, and create them by hand yourself.

I ended up skipping D: and the recovery image and restoring only first 4 partitions. This worked well to boot Windows (but without recovery partition it was not possible to go to safe mode etc).

Now, the most interesting part. I used shell in Clonezilla to create the partitions. With the backup directory mounted, I located a partition table dump made by `sfdisk`. I have commented out last two partitions, and used `sfdisk` to restore the remaining 4 with the dump file. It was very handy to have this file there as I really did not want to know where each partition should start and end.