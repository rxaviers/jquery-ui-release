# Release Checklist

## Getting startet

Make sure AUTHORS.txt is up-to-date. Run this to get a list, sync that with the file:

```
grunt authors
```

Download and run the release script in an empty directory:

```
curl https://raw.github.com/jquery/jquery-ui/[release-branch]/build/release/release.js > release.js && node release.js
```

### Dry Run

To test the release process (it changes all the time), curl the release script, **then change the repo variable** to point at a fork of jquery-ui (it doesn't have to a be a fork, just push it to an empty repo). Afterwards run as mentioned above.

### Fixing A Bad Release

If you screw up, e.g. by forgetting to change the repo variable, and you even pushed the tag or even pushed the master commit, delete the tag before anyone gets a chance to pull it and revert the master commit.
 
### Pre-releases

For a pre-release, run `node release --pre-release {version}` and skip the changelog.

The only CDN that gets updated is the jQuery CDN.

 
## Create Changelog

The release script generates a shell for the changelog along with a dump of all commits and closed tickets. Finalize the changelog and add it to the jqueryui.com repo.
- Add `page/changelog/{version}.md`.
- Modify `page/changelog.md` to include a link to the new changelog. 

If this is a major release, create an upgrade guide.
- Add `page/upgrade-guide/{version}.md`.
- Modify `page/upgrade-guide.md` to include a link to the new upgrade guide.
 
## Update Trac

Edit Trac homepage to link to reports for next version: http://bugs.jqueryui.com/wiki/WikiStart?action=edit

## Update CDNs

### jQuery CDN

TODO: Automate this step.
 1. Upload files (see old release checklist for commands).
 1. Update index.html.
 1. Refresh CDN. 

### Google CDN
 1. Email Google and attach zip.

### Microsoft CDN
 1. Use CDN upload tool and email Microsoft.
 
## jquery-wp-content
 1. Update versions in footer.
 1. Push to GitHub. 
 
## download.jqueryui.com
 1. Update config.json to include the new version. Update the jQuery version if necessary. 
 1. Update version in package.json. 
 1. Commit and push to GitHub.
 1. Publish to npm.
 
## jqueryui.com
 1. Update package.json to use the new version of download.jqueryui.com.
 1. Update changelog and upgrade guide (see above).
 1. Update homepage versions and links.
 1. Add release zip(s) to `/resources/download/`.
 1. Run `grunt build-download create-quickdownload` to create quick download inside `resources/download`, unzip that once to verify the content. 
 1. Commit and push to GitHub .
 
## api.jqueryui.com
 1. Update versions: Search for the previous version number and update all references.
 1. Update the jQuery version if necessary.
 1. Update version in `package.json`.
 1. Commit and push to GitHub.
 
## Finally
 1. Verify results on stage server (pushing to master should've updated everything).
 1. Tag each of the four above and push tags to GitHub.
 1. Verify results on live server.
 
## Write Blog Post
See previous blog post for outline. Pick the right one for major/minor releases.
 1. Use the generated `contributors` file for the list of people to thank. Remove duplicates (mostly username vs full name). Use this to generated comma-separated list: `ruby -e 'puts File.read("contributors").split("\n").join(", ")' | pbcopy`.
 1. Search for the previous version number and update all references.
 1. Reference the right upgrade guide and changelog.
 1. Update the narrative parts, usually the first paragraph.
 1. Save draft, check all links, have someone review it.
 1. Publish!
 
## Tweet about it 
Look at previous release tweets for references. Don't get too creative.
