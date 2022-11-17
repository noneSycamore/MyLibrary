# MyLibrary
> Library to store some Scrips...

## Every time before using
> Remember to pull the repo
```shell
git pull MyLibrary master
```

## Using Mkdocs
```shell
mkdocs serve	% create local service, whitch is lively uploading
mkdocs gh-deploy	% build a static page, and upload to github gh-pages branch
```
> Before using `mkdocs ghdeploy` to update gh-pages branch, 
> Remember to fetch the repo:
```shell
git fetch
```

## Haw to upload
> uploading to Github master
```shell
python3 Scrips_to_md.py
python3 readin.py
python3 filetree.py
git add *
git commit -m 'update'
git push origin master
```

## Now using VScode