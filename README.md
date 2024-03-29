<!--
# license: Licensed to the Apache Software Foundation (ASF) under one
#         or more contributor license agreements.  See the NOTICE file
#         distributed with this work for additional information
#         regarding copyright ownership.  The ASF licenses this file
#         to you under the Apache License, Version 2.0 (the
#         "License"); you may not use this file except in compliance
#         with the License.  You may obtain a copy of the License at
#
#           http://www.apache.org/licenses/LICENSE-2.0
#
#         Unless required by applicable law or agreed to in writing,
#         software distributed under the License is distributed on an
#         "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY
#         KIND, either express or implied.  See the License for the
#         specific language governing permissions and limitations
#         under the License.
-->

Cordova WKWebView Engine Mx
==========================

This plugin makes `Cordova` use the `WKWebView` component instead of the default `UIWebView` component, and is installable only on a system with the iOS 9.0 SDK.

In iOS 9, Apple has fixed the [issue](http://www.openradar.me/18039024) present through iOS 8 where you cannot load locale files using file://, and must resort to using a local webserver. As all the XMLHttpRequests are no longer handled by WKWebView but are processed in native code you don't need to enable CORS on you server. When you need to download files to the device and want WKWebView to be able
to get them by a request (e.g, for images and scripts) you can do that by downloading them to `cordova.wkwebview.storageDir`.

Installation
-----------

This plugin needs cordova-ios >4.0.0.

To install the current release:

    cordova create wkwvtest my.project.id wkwvtest
    cd wkwvtest
    cordova platform add ios@4
    cordova plugin add cordova-plugin-wkwebview-engine-mx

You also must have Xcode 7 (iOS 9 SDK) installed. Check your Xcode version by running:

    xcode-select --print-path

Required Permissions
-----------
WKWebView may not fully launch (the deviceready event may not fire) unless if the following is included in config.xml:
#### config.xml

        <feature name="CDVWKWebViewEngine">
            <param name="ios-package" value="CDVWKWebViewEngine" />
        </feature>

        <preference name="CordovaWebViewEngine" value="CDVWKWebViewEngine" />


Notes
------

On an iOS 8 system, Apache Cordova during runtime will switch to using the UIWebView engine instead of using this plugin. If you want to use WKWebView on both iOS 8 and iOS 9 platforms, you will have to resort to using a local webserver.

We have an [experimental plugin](https://github.com/apache/cordova-plugins/tree/master/wkwebview-engine-localhost) that does this. You would use that plugin instead of this one.

Application Transport Security (ATS) in iOS 9
-----------

The next released version of the [cordova-cli 5.4.0](https://www.npmjs.com/package/cordova) will support automatic conversion of the [&lt;access&gt;](http://cordova.apache.org/docs/en/edge/guide/appdev/whitelist/index.html) tags in config.xml to Application Transport Security [ATS](https://developer.apple.com/library/prerelease/ios/documentation/General/Reference/InfoPlistKeyReference/Articles/CocoaKeys.html#//apple_ref/doc/uid/TP40009251-SW33) directives. Upgrade to the version 5.4.0 to use this new functionality.

Limitations
--------

If you are upgrading from UIWebView, please note there are a number of  limitations of using WKWebView. These can be find at [apache cordova issue tracker](https://issues.apache.org/jira/issues/?jql=project%20%3D%20CB%20AND%20labels%20%3D%20wkwebview-known-issues).

Apple Issues
-------

The `AllowInlineMediaPlayback` preference will not work because of this [Apple bug](http://openradar.appspot.com/radar?id=6673091526656000). This bug [has been fixed](https://issues.apache.org/jira/browse/CB-11452) in [iOS 10](https://twitter.com/shazron/status/745546355796389889).



Supported Platforms
-------------------

- iOS
