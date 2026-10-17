# Storage & maintenance

Your home directory and the astro nodes have little disk space and aren't meant for large files. Store data in the `DiscEvol_storage` folder in your home: about **100 TB**, shared by the group. Keep your files in a personal subdirectory named `name.surname`, and create it if it doesn't exist yet.

!!! warning "Don't `mv` between projects"
    Moving files from another INDACO project into `DiscEvol_storage` with `mv` keeps the old ownership. Use `cp` to copy them over, then `rm` the originals.

## Check storage usage

```bash
du -sh        # size of the current folder
du -h -d N    # sizes of directories up to N levels below
```
