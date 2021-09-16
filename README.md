# bot meeting lifacycle basic - Microsoft Teams App

Teams meeting bot app handling lifecycle events.

## Summary
This sample is a Teams Bot meeting app created using the Teams Yeoman Generator. It acts on the real start and end date (not the scheduled ones) and posts a simple message to the meeting's chat once each event is fired.
App result:

![App result in chat](https://mmsharepoint.files.wordpress.com/2021/09/04meetingbotlifecyleactivities.png)

For further details see the author's [blog post](https://wordpress.com/post/mmsharepoint.wordpress.com/)

## Prerequisites

* [Office 365 tenant](https://dev.office.com/sharepoint/docs/spfx/set-up-your-development-environment)
* [Node.js](https://nodejs.org) version 10.14.1 or higher
* [Gulp CLI](https://github.com/gulpjs/gulp-cli) `npm install gulp-cli --global`
* [ngrok](https://ngrok.com) or similar tunneling application is required for local testing
* Enable Teams Developer Preview in your client via <You Account> | About | Developer Preview

    ```bash
    # determine node version
    node --version
    ```

## Version history

Version|Date|Author|Comments
-------|----|----|--------
1.0|Sep 17, 2021|[Markus Moeller](https://twitter.com/moeller2_0)|Initial release

## Disclaimer

**THIS CODE IS PROVIDED *AS IS* WITHOUT WARRANTY OF ANY KIND, EITHER EXPRESS OR IMPLIED, INCLUDING ANY IMPLIED WARRANTIES OF FITNESS FOR A PARTICULAR PURPOSE, MERCHANTABILITY, OR NON-INFRINGEMENT.**

## Minimal Path to Awesome
- Clone the repository
    ```bash
    git clone https://github.com/mmsharepoint/
    ```

- In a console, navigate to `/tab-meeting-record-name`

    ```bash
    cd tab-meeting-record-name
    ```

- Install modules

    ```bash
    npm install
    ```

- Run ngrok and note down the given url

    ```bash
    gulp start-ngrok
    ```
- You will need to register a Bot Channel for this app by executing the following steps
    - Go to our Azure portal and Bot Services and click "Create"
    - Pick "Azure Bot"
    - Once again click the "Create" button inside
    - Choose a valid name, subscription and resource group
    - Free pricing tier is sufficient in this experimental phase
    - Either create a Microsoft App ID on your own or let the Bot create it for you
    (In the latter case you will get a secret which will be stored in an own Azure Key Vault, pay attention to clean up if you do not use that)
    - Having the bot created, open the resource and under "Channels" add a featured "Teams channel". 
    - Furthermore under Configuration add the following messaging endpoint: https://xxxxx.ngrok.io/api/messages 
    (Later the xxxxx will be exchanged by the real given random ngrok url received)
    - On the "Configuration" tab click "Manage" beside the Microsoft App ID and generate a new secret and note this down
    - Paste App ID and secret into you local .env file got from .env-sample
- Enable Teams Developer Preview in your client via <Your Account> | About | Developer Preview
- Package the app
    ```bash
    gulp manifest
    ```
- Start the app
    ```bash
    gulp serve --debug
    ```
- Create a new teams meeting with at least one participant
- Open the meeting in Edit mode
- At the right end of the tabs click (+) to add a new app and sideload your package
- Join the meeting and after a while leave the meeting


## Useful links
 * [Debugging with Visual Studio Code](https://github.com/pnp/generator-teams/blob/master/docs/docs/vscode.md)
 * [Developing with ngrok](https://github.com/pnp/generator-teams/blob/master/docs/docs/ngrok.md)
 * [Developing with Github Codespaces](https://github.com/pnp/generator-teams/blob/master/docs/docs/codespaces.md)


## Additional build options

You can use the following flags for the `serve`, `ngrok-serve` and build commands:

* `--no-linting` or `-l` - skips the linting of Typescript during build to improve build times
* `--debug` - builds in debug mode
* `--env <filename>.env` - use an alternate set of environment files
* `--publish` - automatically publish the application to the Teams App store

## Deployment

The solution can be deployed to Azure using any deployment method.

* For Azure Devops see [How to deploy a Yo Teams generated project to Azure through Azure DevOps](https://www.wictorwilen.se/blog/deploying-yo-teams-and-node-apps/)
* For Docker containers, see the included `Dockerfile`

## Logging

To enable logging for the solution you need to add `msteams` to the `DEBUG` environment variable. See the [debug package](https://www.npmjs.com/package/debug) for more information. By default this setting is turned on in the `.env` file.

Example for Windows command line:

``` bash
SET DEBUG=msteams
```

If you are using Microsoft Azure to host your Microsoft Teams app, then you can add `DEBUG` as an Application Setting with the value of `msteams`.
