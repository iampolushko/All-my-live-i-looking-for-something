## pyinstaller

```bash
pip install pyinstaller

pyinstaller -F -w main.py
```

U can use a lot of tags and mix it.
The most useful:
**-F** - means build all in one file
**-w** - don't open the console
**-i "full path to ico"** - add ico to program
**--add-data="file\bg.png:."** - to include own files to exe(check more info in google)
