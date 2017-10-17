# Project 7 - WordPress Pentesting

Time spent: **9** hours spent in total

> Objective: Find, analyze, recreate, and document **five vulnerabilities** affecting an old version of WordPress

## Pentesting Report

1. Authenticated Stored Cross-Site Scripting in Youtube URL Embeds
  - [ ] Summary: A cross site scripting vulnerability where code can be executed when attempting to embed a youtube video in a post, given that the post is viewed by another user or admin.
    - Vulnerability types: XSS
    - Tested in version: 4.2
    - Fixed in version: 4.2.13
  - [ ] GIF Walkthrough:
  - [ ] Steps to recreate:
        1. As a contributor, create a post on the site with an embedded youtube video link like "https://youtube.com/watch?v=etc<javascript_code>" where javascript_code is the code you wish the site to run.
        2. Submit the post.
        3. Have a user with privilege access review the code for submission.
        4. As soon as the user loads the post for review, the javascript executes running the code specified.
  - [ ] Affected source code:
    - [Link 1](wpdistillery.dev/wp-admin/post.php)
2. Authenticated Stored Cross-Site Scripting via Image Filename
  - [ ] Summary: Vulnerability given when attempting to upload an image that is too big for a media file. When the size error is given to the user attempting to upload, javascript can be run from the name of the file. This is a linux-unique issue due to placement of code in a file's name in Windows being sanitized.
    - Vulnerability types: XSS
    - Tested in version: 4.2
    - Fixed in version: 4.2.10
  - [ ] GIF Walkthrough:
  - [ ] Steps to recreate:
        1. Create a file with the name of Name_of_File<code_to_be_executed>.png where code_to_be_executed is the javascript code you'd like to execute.
        2. Set the size of the file to be greater than 2 MB using the command 'truncate'.
        3. Attempt to upload the image by creating a new media file and hitting submit.
        4. When the error pops up for the size of the image being too large, the javascript executes.
  - [ ] Affected source code:
    - [Link 1](wpdistillery.dev/wp-admin/media-new.php)
3. Unauthenticated Genericons Cross-Site Scripting
  - [ ] Summary: There exists a vulnerability in a provided library of icons. This html   file, when provided a URL argument containing javascript, can run javascript code on the user's session and execute it immediately.
    - Vulnerability types: XSS
    - Tested in version: 4.2
    - Fixed in version: 4.2.2
  - [ ] GIF Walkthrough:
  - [ ] Steps to recreate:
          1. Navigate to your WPDistillery URL and move to the directory /wp-content/thems/twentyfifteen/genericons/example.html
          2. Tag onto the end of the url "#<malicious_payload>" where malicious payload is the arbitrary javascript you'd want to execute.
          3. Enter the URL and the page will run the javascript.
  - [ ] Affected source code:
    - [Link 1](http://wpdistillery.dev/wp-content/themes/twentyfifteen/genericons/example.html)

## Assets

List any additional assets, such as scripts or files

## Resources

- [WordPress Source Browser](https://core.trac.wordpress.org/browser/)
- [WordPress Developer Reference](https://developer.wordpress.org/reference/)

GIFs created with [LiceCap](http://www.cockos.com/licecap/).

## Notes

Iceweasel had a serious issue exhibiting javascript alerts on Kali for a couple hours, though I finally got around this issue various ways with different browsers and settings.

## License

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

        http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.
