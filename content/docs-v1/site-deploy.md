---
title: Deploy Your Project
weight: 6400
type: essay
abstract: "Learn various methods to preview & deploy your project online"
aliases:
  - /documentation/site-deploy/
---

A Quire site is designed to be hosted on virtually any web server, either one your institution already runs, or a new server from the hosting service of your choice. You do not need any special back-end setup. If you plan to include PDF and e-book files as part of you published project, it's important that you start by following the directions in the [*Output Your Project*](/docs-v1/multiformat-output/) section of the documentation before proceeding.

## Basic Deploy

When hosting a Quire site, you will typically follow these steps:

1. Update the `url` at the top of the `content/_data/publication.yaml` file to match the URL where the site will ultimately be hosted.
2. Create the HTML files for your project by running `quire build` in your command-line shell. The files will be built into your project’s `_site` folder along with all the necessary static assets like image files, stylesheets and script files. The `_site` folder will be updated and overwritten each time you run `quire build`.
3. Upload the contents of the `_site` folder to your web host based on the directions they provide.

If you do not already have a web server or hosting plan, we recommend using either [Netlify](https://www.netlify.com) or [GitHub Pages](https://pages.github.com/).

{{< q-class "box tip" >}}
- Netlify's "Continuous Deployment" option and Github Pages require a basic understanding of how to create a repository, and commit and merge changes changes. If you are new to GitHub, we recommend starting with [GitHub Docs](https://docs.github.com/en/github) to learn by topic or by visiting the [*Project Management with GitHub*](/docs-v1/github) section of our documentation. We also encourage you to check out Coding Train’s video series [Git and Github for Poets](https://www.youtube.com/playlist?list=PLRqwX-V7Uu6ZF9C0YMKuns9sLDzK6zoiV).
{{< /q-class >}}

## Netlify

Netlify enables you to create a quick preview site by using your project's `_site` files or by connecting it with your Github account to generate a shareable preview site that automatically updates every time you push changes to GitHub. (Please note, while we use GitHub and reference it throughout our documentation, you can also link Netlify to your GitLab or BitBucket account.) You can also use Netlify to host your final project when it's ready to publish.

To learn more about connecting domains, build configuration, private submodules, and using Git Large File Storage with Netlify, see [*Additional Netlify Tips*](/docs-v1/netlify/).

To get started, [sign up](https://app.netlify.com/signup) for a Netlify account and, optionally, connect it with your GitHub account.

### Manual Deployment with Netlify

Manual deploy is ideal if you have a small site or want to run a quick preview. You can also use this option without needing a GitHub account. However, each time you make an update, you will need to go through the process of rebuilding the site, compressing files, and reuploading them to Netlify, which may be burdensome if you have a lot of images or larger files. For continuous deployment please see [*Continuous Deployment with Netlify*](#continuous-deployment-with-netlify).

1. When you are ready to launch your project, update the `url` in `contents/_data/publication.yaml` to: `url: 'https://netlify.app'`.

2. Run the `quire build` command in your command-line shell.

3. Navigate to your project in your home directory and compress the `_site` folder.

4. Go to Netlify Drop, [https://app.netlify.com/drop](https://app.netlify.com/drop), and drag-and-drop your compressed `_site` folder into the indicated area.

5. You will be given a randomized default URL to preview your project. Rename this URL by logging into your account, navigating to “Site settings” and changing the site name. You also have the option to buy a domain or set-up a domain you already own.

{{< q-class "box warning" >}}
- Any zooming or layered images will not load properly in your site until you update the `url` in `publication.yaml` to the **full** URL Netlify gives you, or the one you've customized or purchased. Once you finalize the URL you would like to use, update `publication.yaml` and follow the steps below to update your site.
{{< /q-class >}}

If you make further edits to your project and would like to preview them you will need to repeat this process.

1. Delete the old compressed `_site` folder.

2. Run `quire build` again (your files will be automatically overwritten).

3. Compress the newly updated `_site` folder.

4. In Netlify, navigate to “Deploys” at the top of the page. You will see a blank space that reads, “Need to update your site." Simply drag-and-drop your new compressed `_site` folder here and your link will be automatically updated.

{{< q-class "box warning" >}}
- One downside to manual deploys is that they can sometimes get stuck while uploading. To ensure a reliable deploy, use this option for Quire sites under 50MB and avoid individual files over 10MB. It's also recommended that you use the latest version of the Chrome browser. For more tips visit the [Netlify Support Forum](https://answers.netlify.com/t/support-guide-my-drag-and-drop-deploy-is-stuck-in-uploading-status/112).
{{< /q-class >}}

### Continuous Deployment with Netlify

By keeping your project files on GitHub and linking them directly to your Netlify account, any time you merge changes in Github, your preview link will be automatically updated. This process requires a few extra steps to get set-up, but will save time in the long run.

1. If you haven't already, create a repository for your project on GitHub.

2. Log in to [Netlify](https://app.netlify.com/). On the “Team Overview” page, click the button that says “Add new site” and then choose "Import an exisitng project".

3. Next you'll want to “Connect to Git Provider.” Choose the option that best fits your project. You may be asked to "Authorize Netlify". 

4. If you see “No repositories found” you will be prompted to configure Netlify on GitHub.

5. Once this configuration is complete, choose the repository and the branch you would like to preview.

6. Set the "Build command" as `npx @thegetty/quire-cli build` and the "Publish directory" as `_site`.

7. Hit "Deploy Site." Depending on the size of your project, this may take a few moments. Follow along with the build process (and check for errors) by navigating to "Publication Deploys" section and scrolling down to the "Deploy Log".

8. You will be given a randomized default URL to preview your project. Rename this URL by navigating to “Site settings” and changing the site name. You also have the option to buy a domain or set-up a domain you already own. Once you've chosen a final URL, update the `url` in your `content/_data/publication.yaml` file to match. Commit that change and push it to GitHub. Netlify will redeploy the site, and the new URL will ensure all your images, stylesheets, and other assets load properly.

Should you need to make any updates to your site, just merge the changes and Netlify will automatically update your preview link. You can check "Production Deploys" in the site overview section to these track changes.

{{< q-class "box tip" >}}
- Now that you have linked Netlify to your Github account, you'll see notifications about Netlify testing the site each time you submit a new pull request. If the checks pass, you can click the bottom-most link to launch a preview of your site. If the checks fail, there may be broken links, incorrect YAML, or other issues within your project files.
{{< /q-class >}}

## GitHub Pages

GitHub enables you to not only host your project code, but you can also use it to host a live version of your site. Learn more on the [GitHub Pages](https://pages.github.com/) website.

{{< q-class "box warn" >}}
- While the below instructions *should* work we have yet to get a fully functioning deploy to work (*as of March 2023*). So please consider these a starting point, which may need further debugging. And if you do debug it, please let us know so that we can update these instructions for others.
{{< /q-class >}}

### Preview Your Project with Github Pages

1. First, if you haven't already, follow the steps to host your project's code on GitHub in the [*GitHub*](/docs-v1/github) section of our documentation to create a repository for your project.

2. Update the `url` in `content/_data/publication.yaml` to correspond to your own GitHub site. It will follow the pattern: https://YOUR-USERNAME.github.io/YOUR-PROJECT-DIRECTORY-NAME/. So, if your GitHub username is bonjovi and your project file is blaze-of-glory, your `baseURL` would be https://bonjovi.github.io/blaze-of-glory/. (Note: your GitHub username can also be your organization name if that is how your account is set-up in GitHub.)

3. In your command-line shell run `quire build`

4. In the `_site` directory, add an empty file called `.nojekyll`, which lets GitHub know the site you're publsihing [isn't a Jekyll site](https://github.blog/2009-12-29-bypassing-jekyll-on-github-pages/).

5. Next run `git add -f _site && git commit -m "Github pages deploy"` this will add the contents of the `_site` directory to your project's git history so that it can be pushed to GitHub.

6. Run `git subtree push --prefix _site origin gh-pages` to push the committed `_site` files to a new `gh-pages` branch of your repo on GitHub.

7. If your repository is private, you will need to navigate to your repository's settings page. Scroll down to the "Danger Zone," click "Change project visibility" and change the visibility to public.

8. For "Source" switch the branch to `gh-pages` in the `/(root)` folder and save.

9. Your site should now be published at https://YOUR-USERNAME.github.io/YOUR-PROJECT-DIRECTORY-NAME.

If you make changes to your project and want to view them live, you will need to repeat stpes 3–6 above to update your project files and push them to GitHub. Navigate to your GitHub account settings and choose "Pages" from the lefthand menu. Your refreshed link will be at the top of the page. A green box indicates the site has been published and is now live.
