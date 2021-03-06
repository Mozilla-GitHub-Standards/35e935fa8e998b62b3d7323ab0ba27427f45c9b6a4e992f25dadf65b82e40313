## Mozilla Mobile Phonebook README ##

[Atul](http://toolness.com) made this phonebook to scratch two itches:

* Learn how to use [JQuery Mobile](http://jquerymobile.com/).
* Make an offline-capable version of the [Mozilla Phonebook](https://ldap.mozilla.org/phonebook/) with a user interface that's optimized for small screens.

## Prerequisites ##

All you need is Python 2.6 or later, which is used to run scripts that talk to LDAP and cache the Phonebook contents as static files. The actual web app consists entirely of static files.

## Caching The LDAP Phonebook ##

This must be done before you can develop or deploy the app.

First, create a file in the root directory of the repository called `config.json`. Paste the following into it and edit as necessary:

    {
      "username": "my_username@mozilla.com",
      "password": "my_password"
    }

Then run `fetch.py`, followed by `combine.py`.

## Development ##

If you're going to be changing any HTML, CSS, or JavaScript content, delete the `static-files/cache.manifest` file, which is created by `combine.py`. This will cause the browser to obsolete the application cache and ensure that you're always looking at the latest version of your code when you reload the page.

Then, run `server.py` and browse to [http://localhost:8001/](http://localhost:8001/).

## Updating ##

Run `fetch.py` followed by `combine.py`. This will refresh all phone numbers
and employee information, and it will attempt to fetch thumbnails for all
employees that haven't yet submitted a photo. If you want to update all
photos, delete the `static-files/images/people` directory before running
`fetch.py`.

## Deployment ##

Simply re-run `combine.py` if necessary and serve the contents of the `static-files` folder over HTTPS with some kind of access control. You should also make sure that `.manifest` files are served with the MIME type `text/cache-manifest`.
