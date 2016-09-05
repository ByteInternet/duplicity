# Duplicity 0.6.23 with infrequent access storage class

We were running happily on 0.6.23 and wanted to use the infrequent storage class from AWS.
After trying 0.7.10, we found that memory consumption was higher than in 0.6.23.
Hence we backported the infrequent access storage class (it's only 10 lines of code).

# How to update/build this package?

## Checkout master branch
`git checkout master`

## Fetch newest upstream (here as example 0.6.26)
`wget http://mirror.yannic-bonenberger.com/nongnu/duplicity/duplicity-0.6.26.tar.gz`

## Extract into master branch
`tar xvzf duplicity-0.6.26.tar.gz`

## Fix path locations and commit to master
git add .
git commit -m "imported upstream version X"

## Checkout byte branch
git checkout byte

## Rebase onto new master, fix any neccessary merge conflicts
git rebase -i master

## Update changelog
vim debian/changelog

## Build package
gbp buildpackage --git-pbuilder --git-dist=precise --git-arch=amd64 --git-debian-branch=byte
