# GitForFreeCAD

## Cloning a zippey-enabled repo on a new machine
Taking the example of the [GeeXY](https://github.com/pierremtb/GeeXY) project.

```bash
# Install zippey
curl -fLo $HOME/.zippey/zippey.py --create-dirs https://raw.githubusercontent.com/pierremtb/GitForFreeCAD/master/zippey.py
chmod +x $HOME/.zippey/zippey.py
# Clone without checking out (the folder will look empty)
git clone --no-checkout https://github.com/pierremtb/GeeXY
cd GeeXY
# Setup the filter
git config filter.zippey.required true
git config filter.zippey.smudge "$HOME/.zippey/zippey.py d"
git config filter.zippey.clean "$HOME/.zippey/zippey.py e"
# Finally checkout, which will call the .clean function
git checkout --
```

## How does it work?

This hack is pretty smart: git actually detects the binary diffs while you work with the CAD software, so you can see that changes are made on the Source Control of say VS Code, or by running `git status`.

And when staging the files for commit (eg. `git add BeltA.FCStd`), the scripts run and “smudges” the binary file into a git-readable text file.

When checking out a repo (eg. `git pull`), the text files are being “cleaned” back into their FreeCAD-compatible binary format.

## Credits
[zippey](https://bitbucket.org/sippey/zippey/src/master/)
