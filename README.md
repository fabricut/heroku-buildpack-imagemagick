heroku-buildpack-imagemagick
=================================

This is a [Heroku buildpack](http://devcenter.heroku.com/articles/buildpacks) for vendoring the ImageMagick binaries into your project.

This one actually works :)

This fork was made for Fabricut's implementation. We needed to handle some _really_ large images and good luck trying to override the policy file for any other installed version. This modifies the policymap file to increase the default limits and actually lowers the version of ImageMagick to play nice with the rest of our setup.

### Install

In your project root:

`heroku buildpacks:add https://github.com/fabricut/heroku-buildpack-imagemagick  --index 1 --app HEROKU_APP_NAME`

"index 1" means that imagemagick will be installed first.

### Changing version
Go to https://www.imagemagick.org/download/releases and find a version you want (*.tar.gz). Edit the `bin/compile` file and change out the version number. Clear cache, as shown below, and redeploy your app to Heroku.

### Clear cache
Since the installation is cached you might want to clean it out due to config changes.

1. `heroku plugins:install heroku-repo`
2. `heroku repo:purge_cache -app HEROKU_APP_NAME`
