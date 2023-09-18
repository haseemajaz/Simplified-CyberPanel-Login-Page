# Simplified-CyberPanel-Login-Page
Simplified version of the CyberPanel login page, designed with a clean and responsive interface. It provides a user-friendly login experience with form input fields, Google Authenticator support, and error handling.

I made a simplified version of the login page. Maybe there is a slight security benefit also when possible hacker does not know that it is a CyberPanel system.

The file is located at /usr/local/CyberCP/loginSystem/templates/loginSystem/

Making a backup of the original file is recommended. Updating CyberPanel overrides the modified file.

**Get Backup Code here:**

```
<!DOCTYPE html>
<html lang="en">

<head>
    <style>
        .d-flex {
            display: flex;
        }

        .flex-column {
            flex-direction: column;
        }

        .justify-content-between {
            justify-content: space-between;
        }

        .col-login {
            height: 100vh;
            display: flex;
            flex-direction: column;

        }

        .col-login-left {
            background: rgb(51, 204, 204);
            background: -moz-linear-gradient(0deg, rgba(51, 204, 204, 1) 0%, rgba(0, 0, 122, 1) 100%);
            background: -webkit-linear-gradient(0deg, rgba(51, 204, 204, 1) 0%, rgba(0, 0, 122, 1) 100%);
            background: linear-gradient(0deg, rgba(51, 204, 204, 1) 0%, rgba(0, 0, 122, 1) 100%);
            filter: progid:DXImageTransform.Microsoft.gradient(startColorstr="#33cccc", endColorstr="#00007a", GradientType=1);
            justify-content: space-between;
        }

        .form-group .input-group select.form-control,
        .form-group .input-group input.form-control,
        button.btn.btn-login {
            height: 45px;

        }

        button.btn.btn-login {
            background-color: rgb(51, 204, 204);
            box-shadow: 0 0px 0px rgba(0, 0, 0, 0), 0 1px 2px rgba(0, 0, 0, 0);
            transition: all 0.3s cubic-bezier(.25, .8, .25, 1);
        }

        button.btn.btn-login:hover {
            box-shadow: 0 1px 3px rgba(0, 0, 0, 0.12), 0 1px 2px rgba(0, 0, 0, 0.24);
        }

        .form-group .input-group select.form-control:focus,
        .form-group .input-group input.form-control:focus,
        button.btn.btn-login {
            border: 1px solid rgb(51, 204, 204);
        }

        .col-login-right {
            background: #ffffff;
            justify-content: center;
        }

        .col-login-right .login-wrapper {
            display: flex;
            flex-direction: column;
            justify-content: space-around;
        }

        a.login-changelogs {
            border-top: 1px solid #fff;
        }

        .login-changelogs .card {
            padding: 1em;
            background-color: #fff;
            border-radius: 8px;
            box-shadow: 0 1px 3px rgba(0, 0, 0, 0.12), 0 1px 2px rgba(0, 0, 0, 0.24);
            transition: all 0.3s cubic-bezier(.25, .8, .25, 1);
        }

        .login-changelogs .card:hover {
            color: rgb(51, 204, 204);
            box-shadow: 0 12px 24px rgba(0, 0, 0, 0.16), 0 10px 10px rgba(0, 0, 0, 0.18);
        }

        .card-body {
            padding-left: 15px;
        }

        .object-fit {
            height: 100%;
            width: 100%;
            object-fit: cover;
            border-radius: 6px;
        }

        h4.card-learnmore {
            margin-top: 15px;
            position: relative;
            color: rgb(51, 204, 204);
            font-weight: 500;
            font-size: 1.2em;

        }

        h4.card-learnmore span {
            display: inline;
            padding-bottom: 4px;
            border-bottom: 1px solid rgb(51, 204, 204);
        }

        .alert.alert-danger {
            text-align: center;
            margin: 1em 2em 1em 2em;
            padding-top: 1em;
            padding-bottom: 1em;
            border: 1px solid red;
        }


        /* Loading Spinner */
        .spinner {
            margin: 0;
            width: 70px;
            height: 18px;
            margin: -35px 0 0 -9px;
            position: absolute;
            top: 50%;
            left: 50%;
            text-align: center
        }

        .spinner > div {
            width: 18px;
            height: 18px;
            background-color: #333;
            border-radius: 100%;
            display: inline-block;
            -webkit-animation: bouncedelay 1.4s infinite ease-in-out;
            animation: bouncedelay 1.4s infinite ease-in-out;
            -webkit-animation-fill-mode: both;
            animation-fill-mode: both
        }

        .spinner .bounce1 {
            -webkit-animation-delay: -.32s;
            animation-delay: -.32s
        }

        .spinner .bounce2 {
            -webkit-animation-delay: -.16s;
            animation-delay: -.16s
        }

        @-webkit-keyframes bouncedelay {

            0%,
            80%,
            100% {
                -webkit-transform: scale(0.0)
            }

            40% {
                -webkit-transform: scale(1.0)
            }
        }

        @keyframes bouncedelay {

            0%,
            80%,
            100% {
                transform: scale(0.0);
                -webkit-transform: scale(0.0)
            }

            40% {
                transform: scale(1.0);
                -webkit-transform: scale(1.0)
            }
        }
    </style>
    <meta charset="UTF-8">
    <!--[if IE]>
    <meta http-equiv='X-UA-Compatible' content='IE=edge,chrome=1'><![endif]-->
    <title> Login - CyberPanel </title>
    <meta name="description" content="Login to your CypberPanel account">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">

    <!-- Favicons -->
    {% load static %}

    <link rel="stylesheet" type="text/css" href="{% static 'baseTemplate/assets/finalLoginPageCSS/allCss.css' %}">

    <!-- HELPERS -->

    <!-- ELEMENTS -->

    <!-- ICONS -->

    <!-- Admin theme -->

    <!-- Components theme -->

    <!-- JS Core -->

    <script type="text/javascript" src="{% static 'baseTemplate/assets/js-core/jquery-core.min.js' %}"></script>

    <script type="text/javascript">
        $(window).load(function () {
            setTimeout(function () {
                $('#loading').fadeOut(400, "linear");
            }, 300);
        });
    </script>

    <!-- JS Ends -->

    <style type="text/css">
        html,
        body {
            height: 100%;
            background: #ffffff;
        }
    </style>

    <style>
        {{ cosmetic.MainDashboardCSS | safe }}
    </style>

</head>

<body>
<div id="loading">
    <div class="spinner">
        <div class="bounce1"></div>
        <div class="bounce2"></div>
        <div class="bounce3"></div>
    </div>
</div>

<div class>
    <div class="col-md-6 col-sm-12 hidden-md col-login col-login-left">
        <div class="row panel-body my-30" style="padding-bottom: 0px;">
            <div class="col-lg-6 col-md-12 panel-body">
                <h2 class="text-transform-upr text-white my-30 text-bold">WEB HOSTING CONTROL PANEL
                    </br />FOR EVERYONE

                </h2>
                <h4 class="text-white">Powered By OpenLiteSpeed/LiteSpeed Enterprise. Built For Speed, Security and
                    Reliability.</h4>
            </div>
            <div class="col-lg-6 col-md-12 text-center panel-body">
                <img class="" src="/static/images/cyberpanel-banner-graphics.png" alt="" width="96%">
            </div>
        </div>
        <div class="row panel-body">
            <div class="row panel-body">
                <a class=" login-changelogs" href="https://go.cyberpanel.net/updates" target='_blank'>
                    <div class="card mb-3" style="max-width: 540px;">
                        <div class="row g-0">
                            <div class="col-md-3">
                                <img src="{% static 'baseTemplate/images/new-design-list-websites-square.png' %}" alt="..."
                                     class="object-fit">
                            </div>
                            <div class="col-md-8 ml-5">
                                <div class="card-body d-flex flex-column justify-content-around">
                                    <h3 class="card-title mb-5 font-weight-bold">Change Logs</h3>
                                    <p class="card-text mt-10">Stay up to date about new releases and features.</p>
                                    <h4 class="card-learnmore">
                      <span>
                        Learn More
                        <i>
                          <svg xmlns="http://www.w3.org/2000/svg" width="14" height="14" aria-hidden="true"
                               focusable="false" data-icon="external-link-alt" role="img" viewBox="0 0 512 512">
                            <path fill="currentColor"
                                  d="M432,320H400a16,16,0,0,0-16,16V448H64V128H208a16,16,0,0,0,16-16V80a16,16,0,0,0-16-16H48A48,48,0,0,0,0,112V464a48,48,0,0,0,48,48H400a48,48,0,0,0,48-48V336A16,16,0,0,0,432,320ZM488,0h-128c-21.37,0-32.05,25.91-17,41l35.73,35.73L135,320.37a24,24,0,0,0,0,34L157.67,377a24,24,0,0,0,34,0L435.28,133.32,471,169c15,15,41,4.5,41-17V24A24,24,0,0,0,488,0Z"/>
                            </svg>
                          </i>
                      </span>
                                    </h4>
                                </div>
                            </div>
                        </div>
                    </div>
                </a>
            </div>
        </div>
    </div>

    <div ng-app="loginSystem" ng-controller="loginSystem" class="col-md-6 col-sm-12 col-login col-login-right" style="">
        <div class="login-wrapper">
            <form id="loginForm" action="/" class="col-md-8 col-md-offset-2">
                <h1 class="text-transform-upr text-center panel-body text-bold"
                    style="padding-bottom: 0px; color: #33CCCC;">
                    <img class="center-block text-center my-20" src="{% static 'baseTemplate/cyber-panel-logo.svg' %}">
                    CyberPanel
                </h1>
                <h4 class="text-muted text-center mb-10">Web Hosting Control Panel</h4>
                <div class="">
                    <div class="mx-30">
                        <div class="content-box-wrapper panel-body my-10 mx-30">
                            <div class="form-group">
                                <div class="input-group">
                                    <input ng-model="username" type="text" class="form-control" name="username"
                                           placeholder="Enter username" required style="height: 45px;">
                                    <span class="input-group-addon bg-blue">
                      <i class="glyph-icon icon-envelope-o"></i>
                    </span>
                                </div>
                            </div>
                            <div class="form-group">
                                <div class="input-group">
                                    <input ng-keypress="initiateLogin($event)" ng-model="password" type="password"
                                           class="form-control" id="password" placeholder="Password" required
                                           name="password" style="height: 45px;">
                                    <span class="input-group-addon bg-blue">
                      <i class="glyph-icon icon-unlock-alt"></i>
                    </span>
                                </div>
                                <img id="verifyingLogin" class="center-block" src="{% static 'baseTemplate/images/loading.gif' %}">
                            </div>

                            <div ng-hide="verifyCode" class="form-group">
                                <div class="input-group">
                                    <input ng-model="twofa" type="text" class="form-control" name="twofa"
                                           placeholder="Enter code from Google Authenticator" required
                                           style="height: 45px;">
                                    <span class="input-group-addon bg-blue">
                      <i class="glyph-icon icon-unlock-alt"></i>
                    </span>
                                </div>
                            </div>


                            <div class="form-group">
                                <div class="input-group">
                                    <select ng-model="languageSelection" ng-init="languageSelection='english'"
                                            class="form-control">
                                        <option value="english">English</option>
                                        <option>Bangla</option>
                                        <option>Bosnian</option>
                                        <option>Bulgarian</option>
                                        <option>Chinese</option>
                                        <option>French</option>
                                        <option>German</option>
                                        <option>Greek</option>
                                        <option>Italian</option>
                                        <option>Indonesian</option>
                                        <option>Japanese</option>
                                        <option>Polish</option>
                                        <option>Portuguese</option>
                                        <option>Russian</option>
                                        <option>Spanish</option>
                                        <option>Turkish</option>
                                        <option>Vietnamese</option>
                                    </select>
                                </div>
                            </div>


                            <button type="button" style="background-color: #33CCCC;" ng-click="verifyLoginCredentials()"
                                    class="btn btn-success btn-block  btn-login">Sign In
                            </button>
                        </div>
                    </div>
                </div>
            </form>
            <div id="loginFailed" class="alert alert-danger">
                <p>Could Not Login, Error message: {$ errorMessage $}</p>
            </div>
        </div>
    </div>
</div>
<script src="https://code.angularjs.org/1.6.5/angular.min.js"></script>
<script src="https://code.angularjs.org/1.6.5/angular-route.min.js"></script>
<script src="{% static 'loginSystem/login-system.js' %}"></script>

</body>

</html>
```

**Download Simplified Version of CyberPanel Login Page**

```
<!DOCTYPE html>
<html lang="en">

<head>
  <style>
    .d-flex {
      display: flex;
    }

    .flex-column {
      flex-direction: column;
    }

    .justify-content-between {
      justify-content: space-between;
    }

    .col-login {
      height: 100vh;
      display: flex;
      flex-direction: column;

    }

    .form-group .input-group select.form-control,
    .form-group .input-group input.form-control,
    button.btn.btn-login {
      height: 45px;

    }
    button.btn.btn-login {
      background-color: rgb(51, 204, 204);
      box-shadow: 0 0 px 0px rgba(0, 0, 0, 0), 0 1px 2px rgba(0, 0, 0, 0);
      transition: all 0.3s cubic-bezier(.25, .8, .25, 1);
    }
    button.btn.btn-login:hover {
      box-shadow: 0 1px 3px rgba(0, 0, 0, 0.12), 0 1px 2px rgba(0, 0, 0, 0.24);
    }

    .form-group .input-group select.form-control:focus,
    .form-group .input-group input.form-control:focus,
    button.btn.btn-login {
      border: 1px solid rgb(51, 204, 204);
    }

    .col-md-6 { width: 100% !important; }

    .col-login-right {
      background: #ffffff;
      justify-content: center;
    }

    .col-login-right .login-wrapper {
      display: flex;
      flex-direction: column;
      justify-content: space-around;
    }
    a.login-changelogs {
      border-top: 1px solid #fff;
    }

    .login-changelogs .card {
      padding: 1em;
      background-color: #fff;
      border-radius: 8px;
      box-shadow: 0 1px 3px rgba(0, 0, 0, 0.12), 0 1px 2px rgba(0, 0, 0, 0.24);
      transition: all 0.3s cubic-bezier(.25, .8, .25, 1);
    }

    .login-changelogs .card:hover {
      color: rgb(51, 204, 204);
      box-shadow: 0 12px 24px rgba(0, 0, 0, 0.16), 0 10px 10px rgba(0, 0, 0, 0.18);
    }
    .card-body {
      padding-left: 15px;
    }

    .object-fit {
      height: 100%;
      width: 100%;
      object-fit: cover;
      border-radius: 6px;
    }

    h4.card-learnmore {
      margin-top: 15px;
      position: relative;
      color: rgb(51, 204, 204);
      font-weight: 500;
      font-size: 1.2em;

    }

    h4.card-learnmore span {
      display: inline;
      padding-bottom: 4px;
      border-bottom: 1px solid rgb(51, 204, 204);
    }
    .alert.alert-danger {
      text-align: center;
      margin: 1em 2em 1em 2em;
      padding-top: 1em;
      padding-bottom: 1em;
      border: 1px solid red;
    }


    /* Loading Spinner */
    .spinner {
      margin: 0;
      width: 70px;
      height: 18px;
      margin: -35px 0 0 -9px;
      position: absolute;
      top: 50%;
      left: 50%;
      text-align: center
    }

    .spinner>div {
      width: 18px;
      height: 18px;
      background-color: #333;
      border-radius: 100%;
      display: inline-block;
      -webkit-animation: bouncedelay 1.4s infinite ease-in-out;
      animation: bouncedelay 1.4s infinite ease-in-out;
      -webkit-animation-fill-mode: both;
      animation-fill-mode: both
    }

    .spinner .bounce1 {
      -webkit-animation-delay: -.32s;
      animation-delay: -.32s
    }

    .spinner .bounce2 {
      -webkit-animation-delay: -.16s;
      animation-delay: -.16s
    }

    @-webkit-keyframes bouncedelay {

      0%,
      80%,
      100% {
        -webkit-transform: scale(0.0)
      }

      40% {
        -webkit-transform: scale(1.0)
      }
    }

    @keyframes bouncedelay {

      0%,
      80%,
      100% {
        transform: scale(0.0);
        -webkit-transform: scale(0.0)
      }

      40% {
        transform: scale(1.0);
        -webkit-transform: scale(1.0)
      }
    }
  </style>
  <meta charset="UTF-8">
  <!--[if IE]><meta http-equiv='X-UA-Compatible' content='IE=edge,chrome=1'><![endif]-->
  <title>Login</title>
  <meta name="description" content="Login to your CypberPanel account">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">

  <!-- Favicons -->
  {% load static %}

  <link rel="stylesheet" type="text/css" href="{% static 'baseTemplate/assets/finalLoginPageCSS/allCss.css' %}">

  <!-- HELPERS -->

  <!-- ELEMENTS -->

  <!-- ICONS -->

  <!-- Admin theme -->

  <!-- Components theme -->

  <!-- JS Core -->

  <script type="text/javascript" src="{% static 'baseTemplate/assets/js-core/jquery-core.min.js' %}"></script>

  <script type="text/javascript">
    $(window).load(function() {
      setTimeout(function() {
        $('#loading').fadeOut(400, "linear");
      }, 300);
    });
  </script>

  <!-- JS Ends -->

  <style type="text/css">
    html,
    body {
      height: 100%;
      background: #ffffff;
    }
  </style>

</head>

<body>
  <div id="loading">
    <div class="spinner">
      <div class="bounce1"></div>
      <div class="bounce2"></div>
      <div class="bounce3"></div>
    </div>
  </div>

  <div class>
    <div ng-app="loginSystem" ng-controller="loginSystem" class="col-md-6 col-sm-12 col-login col-login-right">
      <div class="login-wrapper">
        <form id="loginForm" action="/" class="col-md-8 col-md-offset-2">
          <div class="" style="display: flex;align-content: center;align-items: center;justify-content: center;">
            <div class="mx-30">
              <div class="content-box-wrapper panel-body my-10 mx-30">
                <div class="form-group">
                  <div class="input-group">
                    <input ng-model="username" type="text" class="form-control" name="username" placeholder="Enter username" required style="height: 45px;">
                    <span class="input-group-addon bg-blue">
                      <i class="glyph-icon icon-envelope-o"></i>
                    </span>
                  </div>
                </div>
                <div class="form-group">
                  <div class="input-group">
                    <input ng-keypress="initiateLogin($event)" ng-model="password" type="password" class="form-control" id="password" placeholder="Password" required name="password" style="height: 45px;">
                    <span class="input-group-addon bg-blue">
                      <i class="glyph-icon icon-unlock-alt"></i>
                    </span>
                  </div>
                  <img id="verifyingLogin" class="center-block" src="{% static 'images/loading.gif' %}">
                </div>

                <div ng-hide="verifyCode" class="form-group">
                  <div class="input-group">
                    <input ng-model="twofa" type="text" class="form-control" name="twofa" placeholder="Enter code from Google Authenticator" required style="height: 45px;">
                    <span class="input-group-addon bg-blue">
                      <i class="glyph-icon icon-unlock-alt"></i>
                    </span>
                  </div>
                </div>


<!--
                <div class="form-group">
                  <div class="input-group">
                    <select ng-model="languageSelection" ng-init="languageSelection='english'" class="form-control">
                      <option value="english">English</option>
                      <option>Bangla</option>
                      <option>Bosnian</option>
                      <option>Bulgarian</option>
                      <option>Chinese</option>
                      <option>French</option>
                      <option>German</option>
                      <option>Greek</option>
                      <option>Italian</option>
                      <option>Indonesian</option>
                      <option>Japanese</option>
                      <option>Polish</option>
                      <option>Portuguese</option>
                      <option>Russian</option>
                      <option>Spanish</option>
                      <option>Turkish</option>
                      <option>Vietnamese</option>
                    </select>
                  </div>
                </div>
-->

                <button type="button" style="background-color: #33CCCC;" ng-click="verifyLoginCredentials()" class="btn btn-success btn-block  btn-login">Sign In
                </button>
              </div>
            </div>
          </div>
        </form>
        <div id="loginFailed" class="alert alert-danger">
          <p>Could Not Login, Error message: {$ errorMessage $}</p>
        </div>
      </div>
    </div>
  </div>
  <script src="https://code.angularjs.org/1.6.5/angular.min.js"></script>
  <script src="https://code.angularjs.org/1.6.5/angular-route.min.js"></script>
  <script src="{% static 'loginSystem/login-system.js' %}"></script>

</body>

</html>
```
**Features:**

Clean and responsive design.
Username and password input fields.
Support for Google Authenticator two-factor authentication.
Error message display for login failures.
Option to choose the preferred language (currently commented out).
Stylish loading spinner during page load.
Utilizes AngularJS for dynamic behavior.

**File Structure:**

index.html: The main HTML file for the login page.
static/: Contains static assets such as CSS and JavaScript files.
static/baseTemplate/assets/: Additional assets used for styling.
static/images/: Images and icons used in the login page.
loginSystem/: Contains AngularJS scripts for dynamic functionality.

**Getting Started:**

To use this login page:

Clone or download the repository.
Customize the page as needed.
Deploy it to your server.

**Contributions:**

Contributions are welcome! Feel free to fork this repository and submit pull requests to enhance or extend the functionality of the login page.

**License:**

This project is licensed under the MIT License.

Feel free to customize the description and content based on your specific needs and any additional details about the repository.

