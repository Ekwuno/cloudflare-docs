---
pcx-content-type: concept
title: Direct Upload
---

# Direct Upload

With Direct Uploads, you can bring your pre-built assets right to Pages. By using your own CI tooling to handle the build, deploy your website's assets right to the Cloudflare edge.

## Methods to uploading

Once you have your pre-built assets ready, there are two ways to begin uploading: 

1. Using Wrangler CLI 
2. Dragging and dropping 

{{<Aside type= "note">}}
  
Within a project, you can switch between creating deployments with either method. However, at this time, you cannot additionally push changes through your standard git-integration within the same project._

{{</Aside>}}

## Supported file types:

* Wrangler: a single folder of assets(e.g. HTML, CSS, JS, PNG, SVG)
* Drag and drop: zip or folder of assets(e.g. HTML, CSS, JS, PNG, SVG) 


## Wrangler CLI 

### Setting up Wrangler: 

To begin, be sure to [install the latest version](https://developers.cloudflare.com/workers/cli-wrangler/install-update/) of Wrangler and [set up Wrangler](https://developers.cloudflare.com/workers/cli-wrangler/authentication/) to work with your Cloudflare user. Please note that Pages integration with Wrangler relies on Wrangler 2.


#### Deploying your first project: 

Execute the following Wrangler command to begin project creation: 

```sh
wrangler pages publish <project directory>
```


Once executed, you will be prompted to choose whether you’d like to publish assets for an existing project or if you’d like to create a new one. To begin a new project, indicate so with the options provided, continue to name your project, and deploy. Subsequent deployments will re-use these values (saved in your `node_modules/.cache/wrangler` folder).

After your first deployment, in the Pages dashboard, you can navigate to your newly created project to access deployment details, including its shareable / unique preview URL. 


#### Creating a new deployment:

Once you’ve deployed your project, you can continue to add new deployments to that project. Deployments will be available at the following convention `<deployment>.<project name>.pages.dev`. 


```sh
wrangler pages publish <directory> --branch=[branch]
```

{{<Aside type= "note">}}

If you are in a git workspace, Wrangler will automatically pull the branch information for you. Otherwise, you will be prompted to choose your branch (which will then determine if the deployment is production or preview).

{{</Aside>}}

#### Other useful commands

If you’d like to use Wrangler to obtain a list of all available projects for direct upload, you can use:

```sh
wrangler pages project list
```

Additionally, if you would like to use Wrangler to obtain a list of all unique preview URLs for a particular project, you can use:

```sh
wrangler pages deployment list
```

For step by step directions on how to use Wrangler and continuous integration tools like GitHub Actions, Circle CI and Travis CI together for continuous deployment, check out our [tutorial](/pages/how-to/)


## Drag and drop


#### Deploying your first project

To begin, on the **Create a Project** page, select **Upload Assets** and enter your project name in the provided field. Your project will be served from `<project name>.pages.dev`. Next drag and drop your build output directory into the uploading frame. Once your files have been successfully uploaded, click **Save and Deploy** and continue to your newly deployed project. 


#### Creating a new deployment

Once you have your project created, select **Create a new deployment** to begin a new version of your site. Next, choose whether your new deployment will be made to your production or preview environment. If choosing preview, you can create a new deployment target or enter an existing one. Deployment targets allow you to access all changes at one preview subdomain with the following convention `<deployment target>.<project name>.pages.dev`. 


## Troubleshooting

When uploading your assets, if an asset exceeds the standard Pages limits of 25 MiB or if the total number of assets exceeds 20k files, you will not be able to deploy your project. 

If using Wrangler, you will see a `Error: Pages only supports files up to 25 MiB in size. <file> is <size> in size` error for asset size exceedance and **"Error: Pages only supports up to 20,000 files in a deployment at the moment. Try a smaller project”** for asset number exceedance. 

If using the drag and drop method, a red warning symbol will appear next to an asset if too large and thus unsuccessfully uploaded. In this case, you may choose to delete that asset but you cannot replace it. To do so, you must reupload the entire project. If you exceed the file number limit, you will receive a {write error message here} error. 
 
