# Using webdav (davfs2) in container
20190228
you need to configure container with privileges as and add device /dev/fuse

```shell
docker run -d -p hostport:containerport --privileged --cap-add SYS_ADMIN --cap-add MKNOD --device /dev/fuse --name you_container name_of_image
```

# Rstudio container

don't forget to use arg -e PASSWORD=your-password

# Rclone use with container

Setup rclone on host and mount with options

But first uncomment `user_allow_other` in /etc/fuse.conf

```
rclone mount remote: /path/to/host --allow_other
```

`--allow_other` allows other users to access the mountpoint
