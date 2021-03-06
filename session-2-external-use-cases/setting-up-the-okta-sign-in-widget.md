# Setting up the Okta Sign-In Widget

## Introduction

The Okta Sign-In Widget is a Javascript widget from Okta that gives
you a fully featured and customizable login experience which
can be used to authenticate users on any web site.

For an example of how the Okta Sign-In Widget works, take a look at the code
below. This code shows you how the quickly add a fully featured
login experience to your web application:

    <head>
      <!-- Core widget js and css -->
      <script src="https://example.okta.com/js/sdk/okta-sign-in-1.0.0.min.js" type="text/javascript"></script>
      <link href="https://example.okta.com/js/sdk/okta-sign-in-1.0.0.min.css" type="text/css" rel="stylesheet">
      <!-- Customizable css theme options. Link your own customized copy of this file or override styles in-line -->
      <link href="https://example.okta.com/js/sdk/okta-theme-1.0.0.css" type="text/css" rel="stylesheet">
    </head>
    <body>
      <div id="okta-login-container"></div>
      <script type="text/javascript">
        var baseUrl = 'https://example.okta.com';
        var oktaSignIn = new OktaSignIn({baseUrl: baseUrl});
    
        oktaSignIn.renderEl(
          { el: '#okta-login-container' },
          function (res) {
            if (res.status === 'SUCCESS') { res.session.setCookieAndRedirect('https://example.okta.com'); }
          }
        );
      </script>
    </body>

Here is what is happening in the code above: 

First, in the `<head>`
tag, we include the  `okta-login.js` Javascript file, which has all
of the logic for the the Okta Sign-In Widget widget. Then, we include the
`okta-login.css` and `okta-theme.css` CSS files, which contain all
of the styling information for the the Okta Sign-In Widget widget.

Secondly, we add a `<div>` tag with an `id` of
`okta-login-container` - you can use any `id` for this tag, but we
use `okta-login-container` here for the sake of clarity.

Lastly, we add Javascript to add the the Okta Sign-In Widget to the
`okta-login-container` tag. In this short example, we are including
this Javascript is included at the end of the file. However, when
you use this code on your own website, you will need to run these
functions in the parts of your code that are run when the DOM is
ready.

The line below initializes the the Okta Sign-In Widget object, note that
the `baseUrl` value **MUST** be the equivalent for your Okta organization.

    var baseUrl = 'https://example.okta.com';
    var oktaSignIn = new OktaSignIn({baseUrl: baseUrl});

The lines below actually render the the Okta Sign-In Widget widget. Note
that the value for `el` can be whatever `id` that you specify, also
note that we only define a "success" callback, in a production
environment, you will want to handle statuses beyond "SUCCESS" and
you will likely also want to define an "error" callback as well.

    oktaSignIn.renderEl(
      { el: '#okta-login-container' },
      function (res) {
        if (res.status === 'SUCCESS') { res.session.setCookieAndRedirect('https://example.okta.com/'); }
      }
    );

Now that you've seen the basics of how to use the Okta Sign-In Widget, it's
time to go into depth on all of the capabilities that it
provides. After we review the capabilities of the Okta Sign-In Widget, we
will then go over how to get started with the widget and how to
customize if for your environment.

Here are the features that the Okta Sign-In Widget provides:

## Authentication

The primary, and most visible use case for the Okta Sign-In Widget is
validating a user using a username and password. In addition to
credential validation the Okta Sign-In Widget also handles validation of
password complexity requirements and displays common error messages
for things like invalid passwords or blank fields. 

## Multi-Factor Authentication

the Okta Sign-In Widget also comes with full support for Multi-Factor
Authentication user flows. It handles enrollment and verification
of factors and comes with built-in support for all of the factors listed below:

-   Okta Verify
-   Google Authenticator
-   RSA SecureID
-   Symantec VIP
-   DUO Security
-   SMS Authentication
-   Security Question

## Self service password reset

the Okta Sign-In Widget has everything you need to give your users the
ability reset their forgotten passwords, it comes with support
for sending reset notifications as well as prompting users to verify
themselves by prompting them to answer a security question.

## Password Expiration

the Okta Sign-In Widget can notify users when their password has expired
and prompt them to update their password before allowing them to
log in.

## Validation and error handling

the Okta Sign-In Widget comes with extensive support for validating user
input as well as handling every imaginable error condition which
might occur in a user login flow.

# Getting started

Now that you have a basic idea of the capabilities in
the Okta Sign-In Widget your next step is to see these capabilities for yourself.
The best way to do this is to set up a version of the
the Okta Sign-In Widget that is configured to point at your own Okta
organization. 

Setting up the Okta Sign-In Widget for your Okta organization requires the
following steps:

1.  Creating an Okta organization
2.  Creating an HTML file with the widget code
3.  Modifying the HTML to use your Okta organization
4.  Copying the HTML file to a web server
5.  Configuring CORS support on your Okta organization

## Creating an Okta organization

You can skip this step if you already have an Okta organization and
have the ability to configure CORS on that Okta organization. 

If you do have the ability to configure CORS for your Okta
organization, or do not have an Okta organization, you will need to 
create an [Okta Developer Edition](https://www.okta.com/developer/signup/) account for yourself before
continuing on the steps below.

## Creating an HTML file with the widget code

The first step of getting the Okta Sign-In Widget set up for your Okta
organization is to copy the HTML below to a file named
`login-to-okta.html` - note that the HTML below is the *absolute minimum* that
you need to get the Okta Sign-In Widget working, it is not a complete
example by any means. A production deployment of the Okta Sign-In Widget
will have a lot more in-depth configuration.

Copy this to a file named `login-to-okta.html` :

    <!doctype html>
    <html lang="en-us">
    <head>
      <meta charset="utf-8">
      <meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1">
      <meta name="viewport" content="width=device-width, initial-scale=1">
      <title>Example Okta SignIn Widget</title>
    
      <!--[if lt IE 9]>
          <script src="//cdnjs.cloudflare.com/ajax/libs/html5shiv/3.7.2/html5shiv.min.js"></script>
      <![endif]-->
    
      <script src="https://example.okta.com/js/mvc/login/okta-login.js" type="text/javascript"></script>
      <link href="https://example.okta.com/css/login/okta-login.css" type="text/css" rel="stylesheet">
      <link href="https://example.okta.com/css/login/okta-theme.css" type="text/css" rel="stylesheet">
      <link href="https://fonts.googleapis.com/css?family=Open+Sans:400" type="text/css" rel="stylesheet">
    </head>
    <body>
      <!-- Render the login widget here -->
      <div id="okta-login-container"></div>
    
      <!-- Script to init the widget -->
      <script>
        var baseUrl = 'https://example.okta.com';
        var oktaSignIn = new OktaSignIn({baseUrl: baseUrl});
    
        oktaSignIn.renderEl(
          { el: '#okta-login-container' },
          function (res) {
            if (res.status === 'SUCCESS') {
              console.log('User %s succesfully authenticated %o', res.user.profile.login, res.user);
              res.session.setCookieAndRedirect('https://example.okta.com/');
            }
          }
        );
      </script>
    </body>
    </html>

## Modify the HTML for your Okta organization

Once you've copied the HTML above into a file named
`login-to-okta.html`, the next step is for you to use your favorite
text editor to modify `login-to-okta.html`. You will need to
replace all instances of the string `example.okta.com` with the
[fully qualified domain name](https://en.wikipedia.org/wiki/Fully_qualified_domain_name) for your Okta organization. 

NOTE: If you aren't sure what the "fully qualified domain name" for your
Okta organization is, it is simply the "[domain](https://en.wikipedia.org/wiki/Uniform_Resource_Locator#Syntax)" part of the URL
that you use to log in to Okta. For example, if your company name
is "Acme" and you log in to Okta using the
`https://acme.okta.com` then your fully qualified domain name
would be "`acme.okta.com`". Likewise, if you are using an Okta
Developer Edition organization, your domain will be something like
"`dev-12345.oktapreview.com`".

There are four lines that you will need to modify in
`login-to-okta.html`, modify each line, replacing
`example.okta.com` with your fully qualified domain name:

1.  The `<script>` tag for `okta-login.js`:
    
        <script src="https://example.okta.com/js/mvc/login/okta-login.js" type="text/javascript"></script>
2.  The `<link>` tag for `okta-login.css`:
    
        <link href="https://example.okta.com/css/login/okta-login.css" type="text/css" rel="stylesheet">
3.  The `<link>` tag for `okta-theme.css`:
    
        <link href="https://example.okta.com/css/login/okta-theme.css" type="text/css" rel="stylesheet">
4.  The string passed as the `baseUrl` to the `OktaSignIn` constructor:
    
        var oktaSignIn = new OktaSignIn({baseUrl: 'https://example.okta.com'});

## Copy the HTML to a web server

Once you've created a `login-to-okta.html` file, your next step is
get this file hosted on a web server. The web server you use will
depend on your development environment and what you are comfortable
with using. 

If you aren't sure what web server to use, or don't have one set up
already, an easy web server to set up on Mac OS X or GNU/Linux
is the `SimpleHTTPServer` that is included with `python`.

If you have Python installed on your system, you can start the
`SimpleHTTPServer` by running the following command from the same
directory that the `login-to-okta.html` file is located in:

    $ python -m SimpleHTTPServer

**For node**

    $ npm install -g http-server
    
    $ http-server

## Configuring CORS support on your Okta organization

The last step that you'll need to do before you can test out
the Okta Sign-In Widget is to enable CORS for the web server you just set
up.

You can enable CORS by following the steps in our  guide for
[guide for Enabling CORS](http://developer.okta.com/docs/api/getting_started/enabling_cors.html). Configure CORS using the same URL for the
web server you are using to host the HTML for the Okta Sign-In Widget. For
example, if you used the SimpleHTTPServer example above, the URL
you will use will likely be "`http://localhost:8000`" (assuming that the server is
started on TCP port 8000 of your local machine).

## Testing the Okta Sign-In Widget

At this point, you are ready to test the Okta Sign-In Widget. 

Test the Okta Sign-In Widget by loading the URL for the
`login-to-okta.html` file in your favorite web browser.

If you used `SimpleHTTPServer` command above, this URL will be
<http://localhost:8000/login-to-okta.html>

Once you've successfully loaded the the Okta Sign-In Widget widget, it is
time to start exploring the capabilities of the
widget. 

Here are two things for you to try:

1.  Log in using credentials that you are know are invalid. 
    For example: Try using "invalid@example.com" as the user name and
    "invalid" as the password. You should see an error.
2.  Try using a valid user name and password. If everything works,
    you will be redirected to <https://example.com>.
    
    If you are redirected, then it works! Your next step will then
    be to configure the Okta Sign-In Widget for your specific requirements.

# Customization

In the example above, you set up a very basic version of
the Okta Sign-In Widget. Now that you've seen it in action, it's time to
start configuring the widget for your specific needs.

the Okta Sign-In Widget is fully customizable via CSS and Javascript. 
Stylistic customizations, changing the way that the widget looks, is
done via CSS. Customization of widget features, the way that the
widget works, and text labels for the widget are done via Javascript. 

The sections below go into detail on how to customize
the Okta Sign-In Widget using CSS and Javascript.

## Customizing style with CSS

Customization of the look and feel of the the Okta Sign-In Widget is done
via CSS, you will need to write CSS style overloads.

Before you get started, it is useful to know how the widget works,
most important is understanding how the widget gets created. The
the Okta Sign-In Widget widget is created when the `renderEl()` Javascript
method is called. When the the `renderEl()` method is called, the
the Okta Sign-In Widget widget will be created as a `<div>` tag with an
`id` of `okta-login` which will be inserted inside of the tag that
you specified in the `el` option to `renderEl` method.

Here is what the opening tag for the the Okta Sign-In Widget widget will look like:

    <div id="okta-login" class="auth-container main-container no-beacon">

Customization of the HTML surrounding the the Okta Sign-In Widget widget
is up to you. Customization of the widget itself will be done on
the `#okta-login` selector and its child elements.

A full list of the CSS selectors that you can use to style the
the Okta Sign-In Widget widget are in the [okta-theme.css](https://example.okta.com/css/login/okta-theme.css) file. We strongly
urge you to style your widget using only the selectors that are
present in the [okta-theme.css](https://example.okta.com/css/login/okta-theme.css) file, other elements in the widget
will be subject to change and might cause your styling to break in
future versions of the the Okta Sign-In Widget widget.

### Example CSS styling for the the Okta Sign-In Widget widget

Below is some example CSS, which will give you an idea of how you
can style the the Okta Sign-In Widget. You can try out this CSS yourself
by copying the `<style>` tag below into the `<head>` section of
the `login-to-okta.html` file that you created above.

    <style>
      body {
        background-image: url('http://2.bp.blogspot.com/-NYZC_4bJT_s/Tw_0yhJ8yQI/AAAAAAAACbg/81Jxffwgh8o/s1600/1.jpg');
        background-repeat: no-repeat;
        background-position: center center fixed;
        -webkit-background-size: cover;
        -moz-background-size: cover;
        -o-background-size: cover;
        background-size: cover;
      }
    
      #container #okta-login .button {
        color: #ffffff;
        background-color: #3a3f44;
        border-color: #3a3f44;
        background-image: -webkit-linear-gradient(#484e55, #3a3f44 60%, #313539);
        background-image: -o-linear-gradient(#484e55, #3a3f44 60%, #313539);
        background-image: -webkit-gradient(linear, left top, left bottom, from(#484e55), color-stop(60%, #3a3f44), to(#313539));
        background-image: linear-gradient(#484e55, #3a3f44 60%, #313539);
        background-repeat: no-repeat;
        filter: progid:DXImageTransform.Microsoft.gradient(startColorstr='#ff484e55', endColorstr='#ff313539', GradientType=0);
        -webkit-filter: none;
        filter: none;
      }
    </style>

## Customizing widget features and text labels with Javascript

The configuration options that are passed to the `OktaSignIn()`
constructor are used to configure the functionality and text labels
of the the Okta Sign-In Widget widget. An example of how to configure
`OktaSignIn()` is below, followed by a full list of all of the
features and text labels that you can use to configure the Okta Sign-In Widget.

### Example

Below is a working example of a customized the Okta Sign-In Widget widget. You can
see what these customizations do by copying this code into your
`login-to-okta.html` example file and reloading the page in your
web browser. A full list of the supported customization options
are below.

    var oktaSignIn = new OktaSignIn({
      baseUrl: baseUrl,
      logo: 'https://upload.wikimedia.org/wikipedia/en/thumb/7/7e/Oldacmelogo.png/200px-Oldacmelogo.png',
    
      features: {
        securityImage: false,
        rememberMe: true,
        smsRecovery: true,
        selfServiceUnlock: true
      },
    
      helpLinks: {
        help: 'http://acme.example.com/custom/help/page',
        forgotPassword: 'http://acme.example.com/custom/forgot/pass/page',
        unlock: 'http://acme.example.com/custom/unlock/page',
        custom: [
          { text: 'Dehydrated Boulders Support', href: 'http://acme.example.com/support/dehydrated-boulders' },
          { text: 'Rocket Sled Questions', href: 'http://acme.example.com/questions/rocket-sled' }
        ]
      },
    
      // See the contents of the 'okta-theme-1.0.0.css' file for a full list of labels.
      labels: {
        'primaryauth.title': 'Acme Partner Login',
        'primaryauth.username': 'Partner ID',
        'primaryauth.username.tooltip': 'Enter your @ partner.com ID',
        'primaryauth.password': 'Password',
        'primaryauth.password.tooltip': 'Super secret password'
      }
    });

### Configurable features

-   `baseUrl`
    
    The base URL for your Okta organization. Examples base URLs include:
    `https://example.okta.com` and `https://dev-12345.oktapreview.com`.
-   `recoveryToken`
    
    If starting in recovery flow (unlock or forgot pass), pass in the `recoveryToken`.
-   `logo`
    
    Company logo to use in the widget.
-   `features`
    
    The options in the `features` object enable or disable widget
    features via a Boolean `true` or `false`. Features are enabled
    by defining them with `true`, and disabled with `false`. For
    example, to enable display of a users security image, you would
    update your `features` object to look like below:
    
        features: {
            securityImage: true
        }
    
    Here is the full list of features that you can configure:
    
    -   `securityImage`
        
        When set to **true**, this will display the user's security image in the
        login widget.
        
        Defaults to **false**
    -   `rememberMe`
        
        When set to **true**, this will display a checkbox allowing a
        user to enable "Remember me" functionality at login.
        
        Defaults to **true**
    -   `smsRecovery`
        
        When set to **true**, this will allow a users with a configured
        mobile phone number to recovery their password using an SMS.
        
        Defaults to **false**
    -   `selfServiceUnlock`
                TODO Document this
-   `helpLinks`
    
    The options in the `helpLinks` object set alternate links to be
    used for the help links on the Okta Sign-In Widget. 
    
    Here is an example of configuring an alternate help link for the
    link labeled "Help", as well as configuring a custom link with a
    label of "Dehydrated Boulders Support":
    
        helpLinks: {
          help: 'http://acme.example.com/custom/help/page',
          custom: [
            { text: 'Dehydrated Boulders Support', href: 'http://acme.example.com/support/dehydrated-boulders' },
        
          ]
        }
    
    -   `help`
        
        When set to a *string containing a URL*, the value of this
        option will be used as the `href` for the help text labeled
        "Help" by default.
    -   `forgotPassword`
        
        When set to a *string containing a URL*, the value of this
        option will be used as the `href` for the help text labeled
        "Forgot password?" by default.
    -   `unlock`
        
        When set to a *string containing a URL*, the value of this
        option will be used as the `href` for the help text labeled
        "Unlock account?" by default.
    -   `custom`
        
        When set to an *array containing objects* with `text` and
        `href` keys, new links will be added to the help text for
        the Okta Sign-In Widget where the value of the `text` key will be
        used as the text label and the value of the `href` key will be
        used as the `href` link that label points to. For example:
        
            custom: [
              { text: 'Dehydrated Boulders Support', href: 'http://acme.example.com/support/dehydrated-boulders' },
              { text: 'Rocket Sled Questions, href: 'http://acme.example.com/questions/rocket-sled' }
            ]