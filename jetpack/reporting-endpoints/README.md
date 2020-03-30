# Partners REST API Endpoint Documentation

We are developing a partner portal that provides aggregate and site-level reporting about the plans that a hosting partner has provisioned. But, this partner portal is not currently available for partners and we do not have a date for it at the moment. That being said, while the partner portal is not usable itself, the endpoints are accessible for hosting partners by querying the REST API endpoints that power the partner portal.

This document details how to get setup to query these endpoints.

## Endpoints

- [Activations List](activations-list.md)
- [Activations Summary](activations-summary.md)
- [Past Invoices](invoices-past.md)
- [Upcoming Invoices](invoices-upcoming.md)

## Authentication

To retrieve reports via the WordPress.com API, you'll need to authenticate with a bearer token that was authorized by the WordPress.com user attached to your partner keys. The way that authentication is handled for these reporting endpoints is different than how authorization works for provisioning and cancelling plans.

Why the different authentication you ask? The reasoning for this is that the `/jpphp` endpoints for provisioning and cancelling plans are meant to be used without explicit user authentication, specifically without requiring that end users authenticate via OAuth before provisioning a plan to the site. Whereas, for these reporting endpoints, we want to be sure that the WordPress.com user that is responsible for the hosting partner has authenticated the access.

In order to get a bearer token, there are two methods:

### Via the Jetpack Partner Portal

In order to get your bearer token via the Jetpack Partner Portal:

- Navigate to the Jetpack Partner's portal
- Open your browser's developer console and paste in the following to get your Bearer token:

    ```javascript
    localStorage.getItem( 'wp_oauth' );
    ```

This is the simpler option, but the Jetpack Partner Portal is currently for internal use only. Jetpack partners will need to use the OAuth method below for the time being.

### Via OAuth

Retrieving a bearer token via OAuth requires a few steps, but with the steps below, it shouldn't take very long.

First, you'll need to be able to login to WordPress.com with the WordPress.com user that is tied to your Jetpack hosting partner. For hosting partners, this user would have been supplied to Automattic by your company when we created your keys to connect to the provisioning API. If you are not sure what the user is, feel free to reach out in Slack or via email and we will assist you with that.

Second, to get authenticated with OAuth, you'll need to create an applicaton on WordPress.com. You can do that by going to [https://developer.wordpress.com/apps/new/](https://developer.wordpress.com/apps/new/). You may set the values to anything that you'd like. But, we'd recommend that you use `http://127.0.0.1:3210` for the redirect and website URL if you'd like to use the script we have below.

After you create your application, make note of the client ID and client secret. We'll need those to actually authenticate. Below, we'll provide a script along with steps to authenticate, but if you'd rather not use the script, you can find documentation for retrieving a bearer token here:

[https://developer.wordpress.com/docs/oauth2/](https://developer.wordpress.com/docs/oauth2/)

#### Script for Retrieving a Bearer Token

In order to retrieve a bearer token for the WordPress.com API without writing much code, we have provided the script below. Assuming that you've already logged in to the correct WordPress.com account, we expect that the following steps will take a few minutes.

- On your desktop, create a directory
- In this directory, create a PHP file named `index.php`
- In that file place:

    ```php
    <?php

    // Configuration: Add your client ID and secret here.
    $client_id     = 'YOUR_CLIENT_ID_HERE';
    $client_secret = 'YOUR_CLIENT_SECRET_HERE';

    if ( ! empty( $_GET['do_redirect'] ) ) {
        $redirect_url = sprintf(
        'https://public-api.wordpress.com/oauth2/authorize?client_id=%d&response_type=code&    redirect_uri=http%%3A%%2F%%2F127.0.0.1%%3A3210&scope=global',
            $client_id
        );
        header( "Location: $redirect_url" );
        die();
    }

    header( 'Content-Type: application/json' );

    $curl = curl_init( 'https://public-api.wordpress.com/oauth2/token' );

    curl_setopt( $curl, CURLOPT_POST, true );
    curl_setopt( $curl, CURLOPT_POSTFIELDS, array(
        'client_id'     => $client_id,
        'redirect_uri'  => 'http://127.0.0.1:3210',
        'client_secret' => $client_secret,
        'code'          => $_GET['code'],
        'grant_type'    => 'authorization_code'
    ) );

    curl_setopt( $curl, CURLOPT_RETURNTRANSFER, 1);

    $auth       = curl_exec( $curl );
    echo $auth;
    ```

- Be sure to change `$client_id` and `$client_secret` to the appropriate values for your WordPress.com application
- Change to the directory that was created earlier and run `php -S '127.0.0.1:3210' -t .` in order to start up a test server
- Navigate to `http://127.0.0.1:3210?do_redirect=1`
- Click the blue "Approve" button
- You should then be redirected back to `127.0.0.1:3210` with some JSON output
- The value for the `secret` key is used for your bearer token
