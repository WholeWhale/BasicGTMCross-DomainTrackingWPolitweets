# Whole Whale GTM Basic Formula With Politweets

The file is meant to be a ready-set starting point to set basic analytics tracking on multiple sites through a single Google Tag Manager container and multiple property ids instead of views as well as implementing the script from [Politweets by Whole Whale](https://app.politweets.org) which helps your visitors, donors, and supporters to reach out to their representatives through Tweeter on the subjects that matter most to your cause.

Make sure you have a property for each site that you will connect and one standalone cross-domain property, and make sure that each site has the same container's GTM script.
   
## Formula Contents

### Variables

* Google Analytics Settings: 
You will need to add your cross-domain Google Analytics(GA) property ID. Already connected to the currently existing tags, it is a reusable option to not have to rewrite any general settings that your tag would share with others
* Cross-Domain Google Analytics Settings: 
Already connected to the currently existing tags, it is a reusable option to not have to rewrite any general settings that your tag would share with others
* PII Scrubber:
You will need to edit the code by replacing `?!youremail\.com` and `?youremail\.com` with the domain name of your sites email (make sure to keep the back slash before the dot).
to use this variable, edit the Google Analytics Settings variable. Under "more settings" > "fields to set" add a field and fill in `customTask` under name, and `{{PII Scrubber}}`under value.
* Cross-domain GA Propety ID: 
This variable is meant to provide the property id related to the visited page. It will check the corresponding hostname on the browser to the assigned ones on the variable and return the assigned property id. For it to work, under the `input` column you will fill the fields with the sites hostnames and fill in the related property id across from it under the `output` column 

Ie.

|`Input`         |          `Output`|
|-----------------|------------------|
|www.wholewhale.com |       UA-XXXX123|
|sample.wholewhale.com  |   UA-XXXX321|
|ie.wholewhale.com   |      UA-XXXX231|

* Auto-Link Domains: 
This variable makes it easy to edit how many URL domains we need to account for like in the Cross-domain GA Property ID. In this case you only need to provide a **comma separated** list of URLS: `www.wholewhale.com,sample.wholewhale.com,ie.wholewhale.com`

### Triggers
If not very acquainted with GTM. Triggers are like sensors (commonly called "listeners")whose solely job is to check if an action has been performed on the page by a visitor and let GTM know that the tags related to it can be executed. Each Trigger relates to an action and it contains certain requirements for it to accept it (called "rules").

* 15 Second Timer: It checks if a visitor has been on the site for 15 seconds
* All Clicks: It checks if anything on the page has been clicked
* All LinksL: It checks if any links have been clicked
* All Outbound Links: it checks if any links outside of the site (AKA that have a different hostname)
* Form Submissions: it checks if a form has been filled and sent
* PDF Click: Checks on clicks to PDF downloadable content
* Scroll Depth: It listents for difenrent percentage ranges that the user had scrolled through the page

### Tags

All tags have a duplicate version. One will send the tracking data to the visited site's GA Property, and the other is meant to send the same tracking data to the cross-domain property.

* Adjusted Bounce Rate
`Category: visit
Action: 15 Seconds
Label: {{Page Path}}`
* All Link Tracking
`Category: Link Clicks
Action: Page: {{Page URL}}
Label: Link: {{Click URL}} - {{Click Text}}`
* Click Tracking
`Category: All Clicks
Action: Text: {{Click Text}}
Label: Link: Page: {{Page URL}}`

* Google Analytics Pageview

* Outbound Links
`Category: Outbound Links
Action: Click
Label: {{Click URL}}`
* PDF Downloads
`Category: Download
Action: PDF
Label: {{Click URL}}`
* Scroll Depth 
`Category: Scroll Depth
Action: Percentage: {{Scroll Depth Threshold}}
Label: Page URL: {{Page URL}}`
* Politweets

## Installation

After downloading the .json file, under the Admin tab within the GTM container, click `Import Container`, click `Choose Container File` and grab the .json file, then select `existing`, select your default works space, and keep `merge` as the option checked, select rename conflicting tags if your container is not empty and click confirm.

You are now ready to use the tags. Preview and edit as needed. 

To make sure politweets is on your site properly, you will need to also need to place the html `<div>` element provided by [the politweets app](https://app.politweets.org/campaigns) in the location that you will like it to appear on the page, the snippet should look something like so:
```
<div id="wholewhale-polytweet-main" campaign_id="0b000cf0-0000-0000-00fd-cec00000e000" pid="00b0e00d-00fc-0d0e-0e0e-000efe0e00ab"></div>
```
