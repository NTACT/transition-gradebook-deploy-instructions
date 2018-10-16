# Deploying Transition Gradebook to Heroku

### Create an account on Heroku: https://signup.heroku.com/

![Heroku signup page](/images/heroku_signup.png)

### Click the Heroku deploy button in the [Transition Gradebook Server repo](https://github.com/NTACT/transition-gradebook-server)

![Heroku deploy button in Transition Gradebook repo](/images/repo_deploy_button.png)

### Enter a unique name for your Transition Gradebook instance

![Heroku deploy page with name input](/images/heroku_deploy_options.png)

### Click the "Deploy app" button and wait for your app to finish deploying

Once the deployment finishes, your app should be accessable at https://YOUR_APP_NAME.herokuapp.com/. Where `YOUR_APP_NAME` is replaced with the unique name you entered before the deployment.

### Configure the Transition Gradebook server site URL and email (used to send password recovery emails)

1. Create an email account for the app to use
2. Navigate to your app's settings (should be located at https://dashboard.heroku.com/apps/YOUR_APP_NAME/settings)

![Heroku settings tab](/images/heroku_app_settings.png)

3. Click "Reveal Config Vars"

![Heroku config vars](/images/heroku_app_vars.png)

4. Add the following values:

* `EMAIL_ADDRESS` - The email address of the account (ex. `tgb-noreply@yourschool.com` or `abcd@gmail.com`)
* `EMAIL_PASSWORD` - The password for the email account
* `EMAIL_FROM` - The "from" field used for outgoing emails (ex. `Transition Gradebook <tgb-noreply@yourschool.com>`) defaults to the value of `EMAIL_ADDRESS`
* `EMAIL_HOST` - The SMTP server to use (defaults to `smtp.gmail.com`)
* `EMAIL_PORT` - The email server port (defaults to `465`)
* `SITE_URL` - The app domain that Heroku created for your app (ex. https://my-school-transition-gradebook.herokuapp.com/)

Note: The app will still run without configuring these email variables, but the password reset functionality will not work.
