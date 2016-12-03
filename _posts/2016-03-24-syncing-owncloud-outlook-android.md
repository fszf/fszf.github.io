---
id: 619
title: Syncing OwnCloud with Outlook and Android
date: 2016-03-24T16:47:19+00:00
author: Frank S
layout: post
guid: http://frankshin.com/?p=619
permalink: /syncing-owncloud-outlook-android/
mashsb_timestamp:
  - "1480704081"
mashsb_shares:
  - "0"
mashsb_jsonshares:
  - '{"total":0}'
dsq_thread_id:
  - "4690994971"
categories:
  - Linux
tags:
  - android
  - caldav
  - outlook
  - ownbox
  - sync
---
With online connectivity increasing ever so much year by year it is about time I 'sync' my work environment.  I've loaded up an owncloud server on my digital ocean droplet and installed the calendar app.
<h3>Connecting Owncloud with Outlook</h3>
<ol>
	<li>Visit <a href="https://sourceforge.net/projects/outlookcaldavsynchronizer/">here</a></li>
	<li>Extract and run the CalDavSynchronizer.Setup.msi</li>
	<li>Launch Outlook, plugin should be started</li>
	<li>Click on Calendar at bottom of outlook</li>
	<li>To the right of File, Home, Send/Receive, Folder, View is a new view window called CalDav Synchronizer</li>
	<li>Click on it</li>
	<li>Click on Synchronization Profiles</li>
	<li>Set Name to what you wish it to be called</li>
	<li>Outlook Folder should be set to Calendar</li>
	<li>Check Synchronize items immediately after change</li>
	<li>DAV URL you can get by hovering over your calendar name in owncloud via a web browser.  Usually is http://domain-or-ip/remote.php/dav/calendars/owncloudusername/calendarname-1/</li>
	<li>Enter in username for owncloud</li>
	<li>Enter in password for username</li>
	<li>Click on test settings</li>
	<li>The rest you can setup as you wish</li>
</ol>
If it doesn't sync right away, click on CalDav Synchronizer and hit synchronize now.  Also refresh your calendar view in owncloud browser.
<h3>Connecting Owncloud with Android</h3>
In my search for a simple synchronization for android and owncloud I came across this <a href="http://wayneoutthere.com/free-android-caldav-calendar-sync-with-owncloud/">blog post</a>.
<ol>
	<li>Essentially, download or open <a href="https://f-droid.org/">F-droid</a></li>
	<li>Search for Caldav Sync Adapter</li>
	<li>Install</li>
	<li>Go to settings, Accounts</li>
	<li>Add Caldav sync adapter</li>
	<li>Input your ownbox credentials (caldav url, username, password)'</li>
	<li>Save/accept</li>
	<li>From the Settings, Accounts window click on Caldav Sync Adapter</li>
	<li>Slide to enable calendar sync</li>
</ol>
Now you can use the built in google calendar app which will pull in your calendar data.