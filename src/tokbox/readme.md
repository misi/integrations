
## Vonage OpenTok Integration

You can either [build and integrate the package yourself](#build)
or use our [OpenTok QuickStart](#quickstart) where you simply load the observer
libraries from GitHub's CDN and initialize by populating the `observerWsEndPoint` global variable using the
`ObserverRTC.ParserUtil.parseWsServerUrl` helper function.

### Build the package yourself <a name="build"></a>

Follow the steps below to build the package from scratch.

#### Install dependencies

- Make sure we have type script installed in the system
    - `npm install -g typescript`
- Install package dependencies
    - `npm ci`

#### Build library with proper configuration parameter

- Build library. 
  - It will create compiled JavaScript libraries in `dist` folder that we will be able to use with OpenTok.
    -  `npm run build-tokbox`


See the quickstart methodology below for adding this library to your web app.


### OpenTok Quickstart <a name="quickstart"></a>

1. Include core library before including `opentok.js` file in your html page.
   We have a public version hosted on GitHub you can use as shown below,
   or use the library you built from the [build and integrate the package yourself](#opentok-build) instructions.
    
  - Production version
    ```html 
    <script src="https://observertc.github.io/observer-js/dist/latest/observer.min.js"></script>
    ```
  - Developer version
    ```html 
    <script src="https://observertc.github.io/observer-js/dist/latest/observer.js"></script>
    ```
 
2. Define server endpoint in global( window ) scope
    ```html
    <script>
        let observerWsEndPoint = ObserverRTC.ParserUtil.parseWsServerUrl(
            "wss://webrtc-observer.org/",           // observerURL
            {{ServiceUUID}},                        // Add a unique ServiceUUID here
            "opentok-demo",                         // MediaUnitID
            "v20200114"                             // StatsVersion
        );
    </script>
    `````

3. Include the integration library

    You can also use the prebuilt libraries hosted on our GitHub links.
    We recommend the minified version. The unminified version includes extra console logging for debugging purposes.

    - Minified version (recommended):
    ```html 
    <script src="https://observertc.github.io/integrations/dist/v0.1.1/tokbox.integration.min.js"></script>
    ```

    - OR Non-minified version:
    ```html 
    <script src="https://observertc.github.io/integrations/dist/v0.1.1/tokbox.integration.js"></script>
    ```

    - In the end it might look similiar to this
        ```html
        <html>
        <body>
      <!--  
      .....
      .....
      -->      
        <script src="https://observertc.github.io/observer-js/dist/latest/observer.min.js"></script>
        <script>
        let observerWsEndPoint = ObserverRTC.ParserUtil.parseWsServerUrl(
            "ws://localhost:8088/",           // observerURL
            "b8bf0467-d7a9-4caa-93c9-8cd6e0dd7731", // Add a unique ServiceUUID here
            "opentok-demo",                         // MediaUnitID
            "v20200114"                             // StatsVersion
        );
        </script>
        <script src="https://observertc.github.io/integrations/dist/v0.1.1/tokbox.integration.min.js"></script>
        <script src="https://static.opentok.com/v2/js/opentok.js" charset="utf-8"></script>
        ```
      
An example can be found in [OpenTok demo folder](../../__test__/tokbox/index.html).
