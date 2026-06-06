## Redirects

This directory contains redirect pages configured to respond to addresses that generate `301` or `404` [HTTP Status codes](https://en.wikipedia.org/wiki/List_of_HTTP_status_codes). Each redirect page listens for it's _permalink_ address, then answers if that address is requested, then redirect the user to the URL listed in it's redirect setting.

Each page contains settings in its [front matter](https://jekyllrb.com/docs/front-matter/), which control the redirect process independently of other redirect pages. This means that more than one redirect page can redirect to the same resource on the website, but only one redirect page can answer to a specific permalink address.

### How to create a new redirect page.

Each redirect page contains a minimun set of fields required to conduct a page redirect. To create a new redirect, do the following:  

1. Create a copy of `template-redirect.md` redirect file located in this folder.
2. Rename it. `ex: [new_name]-redirect.md`
3. Then update the fields located in the front matter portion of the redirect page you copied. (see: Redirect settings)

> **File location:** redirect files can be located outside of the `_redirects` folder, but as a best practice you should keep them all here in one place under this folder for maintainability reasons.

>**Naming convensions:** A redirect file name should end with `-redirect.md` to make the file self identifying, if placed outside of the _redirects folder.

### Redirect setting

The setting for each redirect page are located in the front matter section of the each redirect page and should look similar to this:

``` yml
---
# Redirect
layout: page
title: PIV Issuer Information
permalink: /piv-i-for-issuers/
redirect: https://www.idmanagement.gov/fpki/notifications/#piv-issuer-information
delaytime: 0
memo: redirect for piv-issuers information
---
```
> **Note:** for the redirect you will always use the full URL for example: `https://www.idmanagement.gov/fpki/notifications/#piv-issuer-information` and for the permalink you will always use the short form of the requested page you are answering for. example: `/piv-i-for-issuers/`

>*Note:* the `---` above and below the fields is required by jekyll as [front matter fencing](https://jekyllrb.com/docs/front-matter/) .

**File Structure**
- `layout:` is the layout file used for this type of page. 
- `title:` the title of the destination page.
- `permalink:` the url of the requested or missing page.
- `redirect:` the full url of the destination page to redirect to. `example: https://www.idmanagement.gov/fpki/`
- `delaytime:` the amount of time in *milliseconds* to wait before sending the user to the destination page. (default: 0)
- `memo:` note for record keeping or providing additional information.

### Testing a new redirect page

Once you have provided these settings, you new redirect is configured and ready for testing. If you are sending the user to an existing page on the IDManagement.gov website, then visiting the permalink of the page you are listening for should redirect you to the existing page on IDManagement.gov.  

> **Note:** since the destination page is the full address on the live website, this is the address you will be directed to, no matter which development environment you are testing in, local or in a branch preview.

### Delay Time

If it has been determined that a delay message needs to be presented to the visitor of a page before sending them to the destination page, do the following.  

Change the `delaytime` in the front matter to the desired amount of time: ( `in milliseconds`):

- `example: 1 second = 1000 milliseconds`
- `10000 = 10 seconds`

Then test your page to make sure the new changes are working. (*see: Testing a new redirect page*) You should land on the redirect page for a secified amount of time, then redirected to the destination page. 

### Delay Message
If a redirect requires a message presented to the user, simply add `markdown` or `HTML` below the include statement in the redirect file, then test your redirect to make sure it functions correctly. 
