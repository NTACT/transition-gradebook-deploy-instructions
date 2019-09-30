# Transition Gradebook Manual Install Instructions

This document describes the process of installing Transition Gradebook on a Linux server.

 **1.** Update your server.

```
sudo apt update
```

 **2.** Set your server’s `NODE_ENV` environmental variable to `production`

```
echo "export NODE_ENV=production" >> ~/.bashrc
source ~/.bashrc
```

 **3.** If they are not already installed, install Git, CURL, and PostgreSQL on your server.

```
sudo apt install git curl postgresql postgresql-contrib
```

 **4.** If they are not already installed, install Node and NPM on your server (v7.2.0 or higher).

```
curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.34.0/install.sh | bash
source ~/.bashrc
nvm install v9.2.0
```

 **5.** Create a PostgreSQL role and database for your system user.

```
sudo -u postgres createuser --interactive
createdb $USER
```

 **6.** Set your PostgreSQL role password.

```
psql -c "ALTER USER \"$USER\" WITH PASSWORD ‘your-password-goes-here’"
```

 **7.** Create the transition gradebook database

```
createdb transition_gradebook
```

 **8.** Add the required configuration environmental variables to your `~/.bashrc` file. Make sure you replace `DB-PASSWORD` with the password you entered in step 8 and `YOUR-TGB-ADMIN-EMAIL`/`YOUR-TGB-ADMIN-EMAIL-PASSWORD` with the email credentials for the account you want to use for password reset emails.

```
echo "export DATABASE_URL=postgres://$USER:DB-PASSWORD@localhost:5432/transition_gradebook" >> ~/.bashrc
echo "export PORT=8080" >> ~/.bashrc
echo "export SITE_URL=https://your-domain-goes-here.com/" >> ~/.bashrc
echo "export EMAIL_ADDRESS=YOUR-TGB-ADMIN-EMAIL@gmail.com" >> ~/.bashrc
echo "export EMAIL_PASSWORD=YOUR-TGB-ADMIN-EMAIL-PASSWORD" >> ~/.bashrc
source ~/.bashrc
```

 **9.** Git clone NTACT/transition-gradebook-server repo on your server.

```
git clone https://github.com/NTACT/transition-gradebook-server.git
```

 **10.** Install Transition Gradebook server dependencies.

```
cd transition-gradebook-server
npm install
```

 **11.** Run database migrations (make sure you're in the `transition-gradebook-server` directory when you run this).

```
npm run migrate
```

 **12.** Run database seeds (make sure you're in the `transition-gradebook-server` directory when you run this).

```
npm run seed
```

 **13.** Install Forever
 
```
npm install --global forever
```

 **14.** Start the server with Forever (make sure you're in the `transition-gradebook-server` directory when you run this).
 
 ```
 forever start index.js
 ```
 
 **15.** If the PORT environment variable is set to 8080 as in the example, the app will be accessed at http://localhost:8080/. If everything seems to start correctly but you are still having issues accessing the app, you can check the logs.
  
 ```
 forever logs
 ```
