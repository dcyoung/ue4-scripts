# ue4-scripts

Setup and utility scripts related to ue4 and gamedev.

## gitea-setup

See [gitea-setup/README.md](gitea-setup/README.md)

## ue4-git-setup.ps1

Assuming the desired content workflow in the repository:

- All content creation files in `$REPO/MediaSrc` (subfolders by type)
  - These are typically in formats e.g. Blender that UE4 doesn't read directly, so outside `Content`
  - These files are added to Git
  - They are also tracked as Git LFS files
  - They are NOT marked as lockable, simply because the tooling for managing locking isn't very good outside of Unreal right now
- When exporting, output (`FBX`, `PNG`, `WAV` etc) goes in `$REPO/Content` (and subfolders)
  - These files are *ignored* in Git because they are derived data
  - UE4 imports them to a `.uasset` which contains all their contents anyway
- Imported content becomes `.uasset` in `$REPO/Content`
  - These files are added to Git
  - They are also tracked as Git LFS files
  - These are also marked as *lockable* in Git LFS

To configure this automatically, run the provided script from a Powershell prompt in the root of your UE4 project.

```
Usage:
  ue4-git-setup.ps1 [[-src:]sourcefolder] [Options]

  -src         : Source folder (current folder if omitted)
               : (should be root of trunk in new repo)
  -dryrun      : Don't perform any actual actions, just report on what you would do
  -help        : Print this help
```
