| loio |
| -----|
| f7cbafc9a76140ec8fc55b51a63cf467 |

<div id="loio">

view on: [help.sap.com](https://help.sap.com/viewer/DRAFT/3237636b137e43519a20ad5513c49ccb/latest/en-US/f7cbafc9a76140ec8fc55b51a63cf467.html) | [demo kit nightly build](https://openui5nightly.hana.ondemand.com/#/topic/f7cbafc9a76140ec8fc55b51a63cf467) | [demo kit latest release](https://openui5.hana.ondemand.com/#/topic/f7cbafc9a76140ec8fc55b51a63cf467)</div>
<!-- loiof7cbafc9a76140ec8fc55b51a63cf467 -->

## Create an index.html File

A minimalistic `index.html` file is needed to test the project configuration. This file contains the OpenUI5 bootstrap and an `sap.m.Text` control that displays the text "**OpenUI5 is loaded successfully!**".

1.  Choose the *New Folder* icon in the header toolbar and enter `src` as the folder name.
2.  Select the newly created folder and create a new `index.html` file inside it by choosing the *New File* icon.
3.  Paste the following code in the newly created `index.html` file and select *Save*:

    **index.html**

    ```lang-html
    <!DOCTYPE html>
    <html>
    	<head>
    		<meta http-equiv="X-UA-Compatible" content="IE=edge">
    		<meta charset="utf-8">
    		<title>SAPUI5 Walkthrough</title>
    		<script
    			id="sap-ui-bootstrap"
    			src="/resources/sap-ui-core.js"
    			data-sap-ui-theme="sap_belize"
    			data-sap-ui-libs="sap.m"
    			data-sap-ui-compatVersion="edge"
                   data-sap-ui-async="true"
                   data-sap-ui-onInit="module:my/app/main"
                   data-sap-ui-resourceRoots='{"my.app": "./"}'
     			></script>
    	</head>
    	<body class="sapUiBody" id="content">
    	</body>
    </html>
    ```

4.  Create new file `main.js` and paste the following code into it:

    **main.js**

    ```lang-js
    sap.ui.define(['sap/m/Text'], function(Text) {
        new Text({
            text: "OpenUI5 is loaded successfully!"
        }).placeAt("content");
    });
    ```


> Note:
> Adapt the path where the resources are located \(`src="/resources/sap-ui-core.js"`\) according to your installation. For OpenUI5 you can use `src="https://openui5.hana.ondemand.com/resources/sap-ui-core.js"`.
> 
> You can use this reference to the latest stable version of OpenUI5 for the tutorial or for testing purposes, but never use this for productive use. In an actual app, you always have to specify an OpenUI5 version explicitly.
> 
> For more information, see [Variant for Bootstrapping from Content Delivery Network](Variant_for_Bootstrapping_from_Content_Delivery_Network_2d3eb2f.md).
> 
> 
