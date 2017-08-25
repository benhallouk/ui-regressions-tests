# UI REGRESSIONS

This is a simple guide that show how UI regressions can be done easily to eliminate time checking UI manually

## Getting started

By default this configuration run on chrome canary browser so make sure you get the latest [chrome canary version from here](https://www.google.com/chrome/browser/canary.html)

Install backstop globally using npm

```sh
npm install -g backstopjs
```

Generate the initial configuration file

```sh
backstop init
```

This will create `backstop_data` folder and `backstop.json` file

It is important to change the configuration to match your testing devices and scenarios

### View port configuration

This is where you specify the targeted screen sizes of your devices (phone, tablet vertical, tablet horizontal)

### Scenarios configuration

The place where you define the urls and the elements to be tested you will need at least one url and one element

### Other configuration

There is also other sections where you can specify the the browser engine and other environmental configuration

This would be the configuration for our example

```js
{
  "id": "test",
  "viewports": [
    {
      "label": "phone",
      "width": 320,
      "height": 480
    },
    {
      "label": "tablet_v",
      "width": 568,
      "height": 1024
    },
    {
      "label": "tablet_h",
      "width": 1024,
      "height": 768
    }
  ],
  "scenarios": [
	  {
		"label": "My Local Test",
		"url": "index.html",
		"hideSelectors": [],
		"removeSelectors": [
		],
		"selectors": [
		  "nav",
		  ".jumbotron",
		  "body .col-md-4:nth-of-type(1)",
		  "body .col-md-4:nth-of-type(2)",
		  "body .col-md-4:nth-of-type(3)",
		  "footer"
		],
		"readyEvent": null,
		"delay": 0,
		"onReadyScript": null,
		"onBeforeScript": null
	  }
  ],
  "paths": {
    "bitmaps_reference": "backstop_data/bitmaps_reference",
    "bitmaps_test": "backstop_data/bitmaps_test",
    "engine_scripts": "backstop_data/engine_scripts",
    "html_report": "backstop_data/html_report",
    "ci_report": "backstop_data/ci_report"
  },
  "engineFlags": [],
  "engine": "chrome",
  "report": ["browser"],
  "debug": false,
  "debugWindow": false
}
```

### Generating reference screenshots

This will create the screenshots for the specified elements relevant to the given url, later on you will compare them on every regression when running the tests, note that a new folder will be created with the images inside `backstopjs_data`

```sh
backstop reference
```

### Testing against the reference screenshots

Now that we have the reference screenshots we can run the tests

```sh
backstop test
```

To find out more about the configuration and the tool visit the [their official repo](https://github.com/garris/BackstopJS)
