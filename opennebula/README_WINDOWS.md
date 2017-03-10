# Customize Windows image to use in MegamVertice/VirtEngine.

## Step 1: Download context script from OpenNebula

"context.ps1" and "startup.vbs" helps to setting up all configuration when booting up the windows image.

 context.ps1 - https://raw.githubusercontent.com/OpenNebula/addon-context-windows/master/context.ps1

 startup.vbs - https://raw.githubusercontent.com/OpenNebula/addon-context-windows/master/startup.vbs

 gulpd.conf - https://raw.githubusercontent.com/megamsys/gitpackager/master/verticegulpd/windows/gulpd.conf

## Step 2: Download MegamVertice/VirtEngine Agent - `gulpd.exe`

"MegamVertice/VirtEngine Agent" is an agent that runs inside the Virtual Machine.

 gulpd.exe - https://raw.githubusercontent.com/OpenNebula/addon-context-windows/master/startup.vbs


## Step 3: Start your windows image in OpenNebula

 We assume that you have running OpenNebula installation with Windows (2008 R2/ 2012) image.

 If you don't have an image then you can download a copy from

-

## Step 4: RDP into Windows instance

  Use the default configured userid & password to start customization.

## Step 5: Configure context script

- Place the downloaded "gulpd.exe" to this directory `C:\Program Files\megam\bin`
- Place the downloaded "context.ps1" to this directory `C:\`
- Place the downloaded "startup.vbs" to this directory `C:\`

## Step 6: Configure "MegamVertice/VirtEngine Agent service"

- Open notepad.exe and create PowerShell script `C:\gulprunner.ps1` with the following content:

```
Start-Process -Filepath "C:\Program Files\megam\bin\gulpd.exe" -ArgumentList "-v start" -RedirectStandardOutput "C:\Program Files\megam\gulpdlogger.log" -RedirectStandardError "C:\Program Files\megam\gulpderror.log" -NoNewWindow

````

- Click `Start > Run` *gpedit.msc* which will open **Local group policy editor**

- {{image}}

- Click `Windos Setting > Scripts(Startup/Shutdown) > Startup > Properties` which will display **Startup Properties**

- {{image}}

- In script tab you can find **Add** button.

- Then browse "C:\context.ps1" file and press **OK**

- Again add one more for **C:\startup.vbs**. Then browse "startup.vbs" file and press **OK**

- And select PowerShell Scripts tab press **Add** button.

- Then browse "C:\gulprunner.ps1" file and press **OK**

## Step 6: Configure gulp.conf file

- Place the downloaded "gulpd.conf" to this directory `C:\Users\Administrator\gulp\bin`

Please update the following code in your `gulpd.conf` as per the site.

- vertice_api = "http://localhost:9000/v2"    // Replace localhost to Gateway IP address
- nsqd = ["localhost:4150"]                  // Replace localhost to NSQD IP address



