# Update Existing owlcms and publicresults Cloud Installations

OWLCMS applications such as [OWLCMS](https://github.com/owlcms/owlcms4-heroku) and its [Public Results Scoreboard](https://github.com/owlcms/publicresults-heroku) are deployed to Heroku using a simple `Deploy to Heroku` button.  But Heroku does not provide an automatic update feature. Hence this program.

## Windows Instructions

1. Download the program for your kind of computer from the [Releases](https://github.com/jflamy/owlcms4-heroku-updater/releases/latest) page.
   - On Windows, you can simply download then double-click on the `updater-windows-64.exe` file. 
   
1. If the user has not used the `heroku` program or this updater on the machine before, a prompt for the Heroku username and password is given. The API token is stored locally so that subsequent updates do not require the password.
2. The program fetches the list of the user's Heroku applications and detects the ones that are for owlcms (currently, `owlcms4` and `publicresults`).
3. Each application is then updated, if needed, to the latest version available (prerelease applications are updated to the latest prerelease, stable applications to the latest stable.)  

## Example

On Windows, a new window will open.  You can see that on first use the Heroku login and password is requested.   If you have other Heroku applications, they are skipped.  Only the owlcms applications have the necessary information needed to do the automatic update.

![image](https://user-images.githubusercontent.com/678663/74204710-348c2480-4c6c-11ea-82d7-4908fabb296c.png)



## Linux and macOS

1. On other platforms (Mac, Linux), the program is run from the command-line.  For example, on Linux, you would open a terminal window and type (wget is on single line, copy the link from the Release page)

     ```bash
   ~$ wget https://github.com/jflamy/owlcms4-heroku-updater/releases/download/1.3.1/updater-linux-64
      		...         
   updater-linux-64              100%[=================================================>]   7.72M  4.39MB/s    in 1.8s
   
   2021-11-18 22:37:27 (4.39 MB/s) - ‘updater-linux-64’ saved [8096545/8096545]
   
   ~$ chmod +x updater-linux-64
   ~$ ./updater-linux-64
   updating ar-wl to 4.25.0-alpha01 ........^C
   ~$ ./updater-linux-64
   		...
   ```
     The process on macOS is the same.

2. If the user has not used the `heroku` program or this updater on the machine before, a prompt for the Heroku username and password is given. The API token is stored locally so that subsequent updates do not require the password.
3. The program fetches the list of the user's Heroku applications and detects the ones that are for owlcms (currently, `owlcms4` and `publicresults`).
4. Each application is then updated, if needed, to the latest version available (prerelease applications are updated to the latest prerelease, stable applications to the latest stable.)  

## Command-line options

By default, on Windows, the program opens a new command-line Window.  If you want to use these you will need to use `-createshell false`

| Option&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description                                                  |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| <nobr>`-noshell`</nobr>                            | if missing, open a new terminal window.  If present, run in the current command-line interface without opening a new window (useful for scripts).  Only works on Windows  (ignored on other platforms) |
| -apikey *keyvalue*                                           | Ignore the Heroku access token currently stored in the home directory `.netrc` (`_netrc` on Windows).  Use instead the token provided. The token can be obtained for a given user from the [User Account](https://dashboard.heroku.com/account) page and using the `Reveal`button at the right of the `API Key` section. |
| -app *appName*                                               | Used together with `-archive`, the name of a single application to be updated.  This is used to revert to a prior version in the event of a glitch. |
| `-archive` *tarball*                                         | The explicit URL of a .tar.gz file to be used to rebuild the application.  Such files are located in the Releases section of owlcms-heroku and publicresults-heroku. |
| `-force`                                               | If present, ignore the version numbers and update to the latest available version. Used to work around a bug in the semantic versioning library that thinks that rc9 is bigger than rc10. |
| `-prerelease` | If present, only prerelease versions will be updated. |
| `-stable` | If present, only stable versions will be updated. |

