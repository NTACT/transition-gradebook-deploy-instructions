# Deploying Transition Gradebook to Heroku

### Create an account on Heroku: https://signup.heroku.com/

![Heroku signup page](/images/heroku_signup.png)

### Fork the [Transition Gradebook Server github repository](https://github.com/NTACT/transition-gradebook-server)

### Click the Heroku deploy button in your forked repository.

![Heroku deploy button in Transition Gradebook repo](/images/repo_deploy_button.png)

### Enter a unique name for your Transition Gradebook instance.

![Heroku deploy page with name input](/images/heroku_deploy_options.png)

### Click the "Deploy app" button and wait for your app to finish deploying.

Once the deployment finishes, your app should be accessable at https://YOUR_APP_NAME.herokuapp.com/. Where `YOUR_APP_NAME` is replaced with the unique name you entered before the deployment.

### Configure the Transition Gradebook server site URL and email (used to send password recovery emails).

1. Create an email account for the app to use
2. Navigate to your app's settings (should be located at https://dashboard.heroku.com/apps/YOUR_APP_NAME/settings)

![Heroku settings tab](/images/heroku_app_settings.png)

3. Click "Reveal Config Vars"

![Heroku config vars](/images/heroku_app_vars.png)

4. Add/update the following values:

* `EMAIL_FROM` - The "from" field used for outgoing emails (ex. `tgb-noreply@yourschool.com`).
* `SITE_URL` - The app domain that Heroku created for your app (ex. https://my-school-transition-gradebook.herokuapp.com/) or your custom domain.

### Merge upstream updates

To merge updates into your forked repository, clone your repository and add the NTACT repository as the `upstream` origin.

```
git clone git@github.com:YOUR_GITHUB_USERNAME/transition-gradebook-server.git
cd transition-gradebook-server
git remote add upstream git@github.com:NTACT/transition-gradebook-server.git
```

Then you can pull the latest commits from the NTACT repo and push them to your forked repo.

```
git pull upstream develop
git push origin develop
```

### Deploy updates

Once you've merged upstream changes into your repo, you'll need to deploy them to your Heroku app. Follow these steps:

1. Navigate to the "Deploy" tab in your Heroku app.
2. Click the Github deployment method.
3. Select your github username from the dropdown.
4. Find for your forked repo (most likely named "transition-gradebook-server").
5. Click "connect"

![Heroku github integration](/images/heroku_github_integration.png)

Once connected, you can enable automatic deploys to have Heroku redeploy automatically when a branch in your fork changes. Alternatively, you can manually deploy.

![Heroku github deployment](/images/heroku_github_deploy.png)

For more information about Heroku deployments and Github integration, see the Heroku docs: https://devcenter.heroku.com/articles/github-integration
