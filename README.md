# Video Recognition Demo

The [Video Recognition][visual_recognition_service] Service uses deep learning algorithms to analyze images for scenes, objects, faces, text, and other subjects that can give you insights into your visual content. You can organize image libraries, understand an individual image, and create custom classifiers for specific results that are tailored to your needs.

Give it a try! Click the button below to fork into IBM DevOps Services and deploy your own copy of this application on Bluemix.


## Getting Started

1. Create a Bluemix Account:

  [Sign up][sign_up] in Bluemix, or use an existing account.

2. Download and install the [Cloud-foundry CLI][cloud_foundry] tool

3. Edit the `manifest.yml` file, and change the `- name: visual-recognition-demo` line to something unique.
  ```yml
  ---
  declared-services:
    visual-recognition-free:
      label: watson_vision_combined
      plan: free
  applications:
  - name: <application-name>
    path: .
    command: npm start
    memory: 512M
    services:
    - visual-recognition-free
    env:
  NODE_ENV: production
  ```
  The name you use determines your initial application URL, e.g. `<application-name>.mybluemix.net`.

4. Connect to Bluemix in the command line tool
  ```sh
  $ cf api https://api.ng.bluemix.net
  $ cf login -u <your user ID>
  ```

5. Create the Visual Recognition service in Bluemix
  ```sh
  $ cf create-service watson_vision_combined free visual-recognition-free
  ```

7. Push it live!
  ```sh
  $ cf push
  ```

See the full [API Reference](http://www.ibm.com/watson/developercloud/visual-recognition/api/v3/) documentation for more details, including code snippets and references.

## Running locally
  The application uses [Node.js](http://nodejs.org) and [npm](https://www.npmjs.com) so you will have to download and install them as part of the steps below.

1. Create a .env file in the root directory of the project with the following content:

    ```none
    API_KEY=<api_key>
    ```
    You can see the `<api_key>` of your application using the `cf env` command:

    ```sh
    $ cf env <application-name>
    ```
    Example output:
    ```sh
    System-Provided:
    {
    "VCAP_SERVICES": {
      "watson_vision_combined": [{
          "credentials": {
            "url": "<url>",
            "api_key": "<api_key>",
          },
        "label": "visual_recognition",
        "name": "visual-recognition-service",
        "plan": "standard"
     }]
    }
    }
    ```

2. Install [Node.js](http://nodejs.org/)
3. Go to the project folder in a terminal and run:
    `npm install`
4. Start the application
5.  `npm start`
6. Go to `http://localhost:3000`

## Troubleshooting

To view your logs and troubleshoot your Bluemix application, run:

  ```sh
  $ cf logs <application-name> --recent
  ```

## Environment Variables

  - `API_KEY` : This is the API key for the vision service, used if you don't have one in your bluemix account.
  - `PRESERVE_CLASSIFIERS` : set if you don't want classifiers to be deleted after one hour.
  - `GOOGLE_ANALYTICS` : set to your google analytics key, if you want analytics enabled.
  - `PORT` : The port the server should run on. This is optional.
  - `OVERRIDE_CLASSIFIER_ID` : if you want to always use a custom
    classifier, you can set that classifier ID in this env var and it
    will be used instead of training a new one.

## Changing the Included Images.



## License

  This sample code is licensed under Apache 2.0. Full license text is available in [LICENSE](LICENSE).

## Contributing

  See [CONTRIBUTING](CONTRIBUTING.md).


### Disabling Deployment Tracking

Deployment tracking can be disabled by removing `require('cf-deployment-tracker-client').track();` from the beginning of the `server.js` file at the root of this repo.

[deploy_track_url]: https://github.com/cloudant-labs/deployment-tracker
[service_url]: http://www.ibm.com/watson/developercloud/visual-recognition.html
[cloud_foundry]: https://github.com/cloudfoundry/cli
[visual_recognition_service]: https://www.ibm.com/watson/developercloud/visual-recognition.html
[sign_up]: https://console.ng.bluemix.net/registration/
[getting_started]: http://www.ibm.com/watson/developercloud/doc/getting_started/



