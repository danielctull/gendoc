Run the gendoc script from the root of your project.

It makes a temporary directory and generates appledoc documentation for your project in that directory.

It then makes a local clone of your documentation branch (called gh-pages, by default), copies the generated appledoc html into a folder in the branch (called Documentation by default), commits the new documentation and pushes it back to the project repo.

At the same time, the script generates an Xcode docset for the documentation, installs it into the right place on your local machine, and includes it in the pages that get uploaded to github, along with an rss feed that can be used to subscribe to the docset.

It then optionally pushes the new documentation back up to github (see Options below).

## Assumptions

This script assumes:
- the name of the root folder is the name of the project
- your appledoc templates are in ~/.appledoc (can be a symlink)
- you have a GlobalSettings.plist file in your appledoc templates folder
- you've set values in GlobalSettings.plist for --project-company, --company-id

The script looks at the remotes configured in the repo to try to work out what your github
user name is, so that it can generate the correct urls for a docset feed.
It looks for the first remote with the pattern: git@github.com:yourname/

## Options

The script looks for a file `.appledoc.plist` at the root of your project. If it finds it, it reads additional appledoc settings from it. You can use this to customise your Appledoc settings on a per-project basis.

There are also currently three options that you can set by editing the top of the script.

Setting `publish` to true causes the generated pages to be pushed back up to github. If it's set to false, the script just echoes out the git command that you would need to use to do the push.

Setting `open` to true opens the index page of the generated documentation in your default browser. Github can take a while to update the pages after you've pushed, so this isn't always a useful thing to do.

Setting `editcommit` to true gives you a chance to edit the message used when committing the generated documentation to the gh-pages branch. I default this to false as these messages tend not to be particularly useful. Typically I will have used a sensible commit message when actually changing the source files from which the documentation is generated, so another commit message just to say that it's been generated tends to be overkill.

One day I might get round to refining the script so that these options can be specified on the command line... one day...

## Credits

From an original script by Daniel Tull.
Somewhat mangled by Sam Deane.
