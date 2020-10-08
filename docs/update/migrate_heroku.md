# Atlas migration is mandatory for Heroku users with mLab.

</br>

!!! warning "You must migrate your existing mLab MongoDB, where all your Nightscout data are stored, to MongoDB Atlas **before November 2020**."
    This is essential to keep your Nightscout functioning.

</br> 

Read this:

[https://github.com/nightscout/cgm-remote-monitor/wiki/mLab-discontinuation-FAQ](https://github.com/nightscout/cgm-remote-monitor/wiki/mLab-discontinuation-FAQ)

To migrate your database you can use the video provided by mLab:

[https://docs.mlab.com/how-to-migrate-nightscout-sandbox-heroku-addons-to-atlas/](https://docs.mlab.com/how-to-migrate-nightscout-sandbox-heroku-addons-to-atlas/)

</br> 

Access your Heroku account from a computer. Do not change device/computer/browser during the upgrade!

!!! note "If you have issues with your current browser try another one."

 </br>

# Important Prerequisite

</br>

[**Update your Nightscout to latest release!**](.\update.md)

 </br>

## Step 1: Heroku

</br>

Click this link to login in Heroku: [**https://id.heroku.com/login**](https://id.heroku.com/login)

Insert mail and password then click Log In

<img src="..\img\MigrateNS00.png" style="zoom:80%;" />

Select your Nightscout app name  

<img src="..\img\MigrateNS01.png" style="zoom:80%;" /> 

Go to Settings

<img src="..\img\MigrateNS02.png" style="zoom:80%;" /> 

Click Reveal Config Vars

<img src="..\img\MigrateNS03.png" style="zoom:80%;" /> 

Scroll down until you’ll find a variable named `MONGO_CONNECTION` or `MONGODB_URI` or `MONGOLAB_URI` or similar. 

This variable has been automatically created at first Nightscout distribution on Heroku. We want to make a backup.

<img src="..\img\MigrateNS04.png" style="zoom:80%;" /> 

Copy the value of this variable, it will look like: `mongodb://heroku_user:password@database.mlab.com:port/heroku_user `

Scroll down Config Vars until you’ll see `KEY` and `VALUE`

<img src="..\img\MigrateNS05.png" style="zoom:80%;" /> 

 In `KEY` write `MONGO_TEMP` then paste in `VALUE` the text copied above, click Add

<img src="..\img\MigrateNS06.png" style="zoom:80%;" /> 

This new key will be inserted at the bottom of the list.

<img src="..\img\MigrateNS07.png" style="zoom:80%;" /> 

!!! info
    If you want, open this [helper link](./stringhelp.html) in another tab, paste this string in the first field then `Validate` it.

Another one…

Scroll down Config Vars until you’ll see `KEY` and `VALUE`

<img src="..\img\MigrateNS08.png" style="zoom:80%;" /> 

 In `KEY` write `MONGO_CONNECTION` (leave the field `VALUE` empty) then click Add

<img src="..\img\MigrateNS09.png" style="zoom:80%;" /> 

This new key will be inserted at the bottom of the list.

<img src="..\img\MigrateNS10.png" style="zoom:80%;" /> 

We’ll use it later. 

Now scroll all the way up and select `Overview` (top left)

<img src="..\img\MigrateNS11.png" style="zoom:80%;" /> 

Click `mLab MongoDB`

<img src="..\img\MigrateNS12.png" style="zoom:80%;" /> 

Another tab will open, from mLab. **Leave it open**. 

<img src="..\img\MigrateNS62.png" style="zoom:80%;" /> 

Go back to Heroku and select `Settings`

<img src="..\img\MigrateNS13.png" style="zoom:80%;" /> 

</br>

## Step 2: Atlas account

Now let’s create an Atlas account.

!!! warning "**Do NOT close Heroku and mLab tabs, they MUST remain opened until the end of the migration.**"

Open another tab at: [https://www.mongodb.com/cloud/atlas](https://www.mongodb.com/cloud/atlas) and click `Start Free`

<img src="..\img\MigrateNS15.png" style="zoom:80%;" /> 

Enter information then click `Get Started Free`

<img src="..\img\MigrateNS16.png" style="zoom:80%;" /> 

Choose a name for your organization or leave default value.

Click `Skip`.

<img src="..\img\MigrateNS17.png" style="zoom:80%;" /> 

Scroll down and click `Dismiss`

<img src="..\img\MigrateNS18.png" style="zoom:80%;" /> 

Click your name, top right, and select `Organizations`.

<img src="..\img\MigrateNS19.png" style="zoom:80%;" /> 

Click on your organization name

<img src="..\img\MigrateNS20.png" style="zoom:80%;" /> 

Click `Settings`.

<img src="..\img\MigrateNS21.png" style="zoom:80%;" /> 

</br>

## Step 3: mLab migration

</br>

Check the mLab tab is still opened. If it’s on a login window, reopen it from Heroku.

Scroll down to `Connect to mLab`

<img src="..\img\MigrateNS22.png" style="zoom:80%;" /> 

<img src="..\img\MigrateNS23.png" style="zoom:80%;" /> 

`Authorize` Atlas to connect to mLab

<img src="..\img\MigrateNS24.png" style="zoom:80%;" /> 

The page will open on the connected mLab deployment

On the right click `...` in actions and select `Configure Migration`

<img src="..\img\MigrateNS25.png" style="zoom:80%;" /> 

Click on `Create or Select Target Project`

<img src="..\img\MigrateNS26.png" style="zoom:80%;" /> 

Click the drop down menu below `Project` and select `Create New Project`

<img src="..\img\MigrateNS27.png" style="zoom:80%;" /> 

Insert your project name (not important) and click `Confirm Project and Continue`

<img src="..\img\MigrateNS28.png" style="zoom:80%;" />         

Click `Import Database Users and Continue`

<img src="..\img\MigrateNS29.png" style="zoom:80%;" /> 

Enable Allow all IP addresses and click `Allow All And Continue`

<img src="..\img\MigrateNS30.png" style="zoom:80%;" /> 

 Click the drop down menu below `Cluster` and select `Create most equivalent new cluster RECOMMENDED`

<img src="..\img\MigrateNS31.png" style="zoom:80%;" /> 

 Click `Confirm Target and Continue`

<img src="..\img\MigrateNS32.png" style="zoom:80%;" /> 

Be patient

<img src="..\img\MigrateNS33.png" style="zoom:80%;" /> 

Click `Confirm Source and Target`

<img src="..\img\MigrateNS34.png" style="zoom:80%;" /> 

Click `Confirm and Continue`

<img src="..\img\MigrateNS35.png" style="zoom:80%;" /> 

Click `Begin Test Run`

<img src="..\img\MigrateNS36.png" style="zoom:80%;" /> 

 Wait for the test to finish (be patient)

<img src="..\img\MigrateNS37.png" style="zoom:80%;" /> 

When available, click `Test Connectivity`

<img src="..\img\MigrateNS38.png" style="zoom:80%;" /> 

!!! warning "Next step is critical"
    Copy the new Atlas string and paste it in a Notepad to avoid losing it.

Click on the `Copy` button.

<img src="..\img\MigrateNS39.png" style="zoom:80%;" /> 

!!! warning "Don’t lose it"
    We’ll need it in Heroku later!

!!! info
    If you opened the helper link above, paste this string in the second field and `Validate` it.

<img src="..\img\MigrateNS40.png" style="zoom:80%;" /> 

Click `Confirm And Continue`

<img src="..\img\MigrateNS41.png" style="zoom:80%;" /> 

!!! warning "Don’t click anything on the next step without reading!"

Click the drop-down menu on the side of `Confirm and Continue` and select `Confirm and Close`!

<img src="..\img\MigrateNS42.png" style="zoom:80%;" /> 

Here we are, we’ll now migrate mLab to Atlas

Click `Review Process and Begin`

<img src="..\img\MigrateNS43.png" style="zoom:80%;" /> 

 Select `I understand …` and click `Begin Migration`

<img src="..\img\MigrateNS44.png" style="zoom:80%;" /> 

Done! Click `Start Using Atlas`

<img src="..\img\MigrateNS45.png" style="zoom:80%;" /> 

!!! note
    Last chance to copy the string...

Click `I’m Done`

<img src="..\img\MigrateNS46.png" style="zoom:80%;" /> 

 Select both `I understand …` and `I am not using …` then click `Confirm and Close `

<img src="..\img\MigrateNS47.png" style="zoom:80%;" /> 

Your window will update, database has been migrated to Atlas

<img src="..\img\MigrateNS48.png" style="zoom:80%;" /> 

</br>

## Step 4: Connection string

 Go back to Settings in Heroku

<img src="..\img\MigrateNS49.png" style="zoom:80%;" /> 

Click `Reveal Config Vars`

<img src="..\img\MigrateNS50.png" style="zoom:80%;" /> 

Scroll down to `MONGO_TEMP`.

<img src="..\img\MigrateNS51.png" style="zoom:80%;" /> 

Copy the contents of your Notepad in a line below your Atlas string.

<img src="..\img\MigrateNS52.png" style="zoom:80%;" /> 

!!!warning "The following operation is critical."
    You must insert the mLab password in your Atlas string.

!!! info
    If you used the helper link above, copy the resulting string obtained by pressing the `Convert` button.

In Notepad you have two strings with this format (not these values).

`mongodb+srv://heroku_zzzzzzzz:<password>@cluster-zzzzzzzz.xxxxx.mongodb.net/heroku_zzzzzzzz?retryWrites=true&w=majority`

`mongodb://heroku_zzzzzzzz:hfo7fbh6h3dummy6o60kvjojg0@yyyyyyyy.mlab.com:12345/heroku_zzzzzzzz`

Your password (do not copy it from this guide) is made of **26 characters** in between **:** and **@**.

In the first string you should replace `<password>`, with your real password so that it will look like this:

`mongodb+srv://heroku_zzzzzzzz:hfo7fbh6h3dummy6o60kvjojg0@cluster-zzzzzzzz.xxxxx.mongodb.net/heroku_zzzzzzzz?retryWrites=true&w=majority`

!!!note
    there are no < and > remaining in this string!

Now find and edit the `MONGO_CONNECTION` variable (click the pen to edit it)

Paste the resulting string and click `Save changes`

<img src="..\img\MigrateNS53.png" style="zoom:80%;" /> 

 Find the variable named `MONGODB_URI` or `MONGOLAB_URI` that you identified at the beginning and click the cross to delete it.

<img src="..\img\MigrateNS54.png" style="zoom:80%;" /> 

Confirm with `Delete Config Var`

<img src="..\img\MigrateNS55.png" style="zoom:80%;" /> 

Scroll up to the page top, still in `Settings`, click `More`, select `Restart all dynos`

<img src="..\img\MigrateNS57.png" style="zoom:80%;" /> 

Congratulations, you completed migration from mLab to Atlas.

Browse to your Nightscout site and wait 5/10 minutes for it to restart (make sure readings are sent to it).

</br>

## Step 5: Update Nightscout

!!! warning "If you didn't update Nightscout before migration"
    [**Update your Nightscout to latest release!**](.\update.md) 
    Versions older than 13.0.x won't probably run. 
    Versions 13.x are not optimized for the Atlas database.

</br>

## Step 6: Delete mLab add-on (optional)

!!! warning "Warning"
    **MAKE SURE NIGHTSCOUT IS FULLY FUNCTIONAL BEFORE REMOVING THE ADD-ON**

If you want to complete the operation once you’re sure everything is working well (**and this is not necessary**) you can remove mLab from Heroku.

For this, in Heroku go to `Resources`

<img src="..\img\MigrateNS58.png" style="zoom:80%;" /> 

 On the right of the mLab MongoDB line, click the drop down menu then `Delete Add-on`

<img src="..\img\MigrateNS59.png" style="zoom:80%;" /> 

Write the name of your app to confirm, click `Remove add-on`

<img src="..\img\MigrateNS60.png" style="zoom:80%;" /> 

 Migration is complete and your Nightscout doesn't have anything to do with the old mLab database now.