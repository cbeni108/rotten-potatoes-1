EdX CS 169.1X Fall 2013

Switch to the rottenpotatoes directory that you've unzipped from the skeleton (see link above)

cd rottenpotatoes

Now you need to install various libraries with the bundle command

bundle install

Now you can test the app locally by running the following and navigating to http://localhost:3000 in your browser

rails s

Now you need to initialize a git repository to put the code in

git init

Then add all the files in the rottenpotatoes directory

git add *

Commit those changes to the local repository

git commit -m "initial commit"

In order to deploy to Heroku you will need to install Heroku Toolbelt on your VM.  First, sign up for a free Heroku account at https://id.heroku.com/signup and follow the instructions to create your account.

Unfortunately there is currently a bug with the Heroku Toolbelt install script on Linux, but you can work around it as follows:

wget --no-check-certificate http://toolbelt.heroku.com/install-ubuntu.sh

The above downloads an installation script, that is made executable with the following command

chmod 775 install-ubuntu.sh

and then can be run with this next command

./install-ubuntu.sh

Now you will likely get the following error: 'E: There are problems and -y was used without --force-yes ' which you can fix with the following: sudo apt-get install -y --force-yes heroku-toolbelt

Assuming you have heroku toolbelt installed you now need to set up ssh keys to securely talk to Heroku.  The three basic commands you need are the following, but see the Heroku page for more details.

ssh-keygen -t rsa

heroku login

heroku keys:add

Once you have your heroku keys set up correctly you can create a heroku instance from the rottenpotatoes directory

heroku create

Now we can use git to deploy our code to the Heroku server in the cloud

git push heroku master

Note, if you see a warning such as:

    The authenticity of host 'heroku.com (50.19.85.132)' can't be established.
    RSA key fingerprint is 8b:48:5e:67:0e:c9:16:47:32:f2:87:0c:1f:c8:60:ad.
    Are you sure you want to continue connecting (yes/no)? 
    Please type 'yes' or 'no':

This is normal - go ahead and type yes then <ENTER> to add heroku to the list of known hosts.

Next we need to tell the cloud instance to prepare the database:

heroku run rake db:migrate

We need to tell the cloud instance to add some data to the database:

heroku run rake db:seed

Now you can navigate to the heroku url that heroku create printed to the console and see your app running in the cloud.

You can find more details on git and Heroku in the appendices of the ESaaS textbook.

====================

[http://frozen-atoll-9538.herokuapp.com](frozen-atoll-9538.herokuapp.com)

Heroku repository:
git@heroku.com:frozen-atoll-9538.git

