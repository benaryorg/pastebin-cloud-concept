Using [Pastebin](http://pastebin.com) as a Cloud
================================================


# Contribution

First of all, if you want to contribute, please send a pull request.

There are some TODOs as HTML comments in the text and here are some more:

- add italics and bold font where appropriate
- add links where useful
- add content
- buy me some cookies for my hard work


# Implementation

If you really want this to be implemented, please contact me
([binary@benary.org](mailto:binary@benary.org)).

If there are enough people who want this, I will build a cross-platform and
open-source client implementing all of this.

# Pastebin

Quoted from their FAQs:

> Pastebin.com is a website where you can **store** text for a certain period of
> time. The website is mainly used by programmers to store pieces of sources
> code or configuration information, but anyone is more than welcome to paste
> any type of text. The idea behind the site is to make it more convenient for
> people to share large amounts of text online.

Here we have the main keyword which led me to the idea, more than once, to use
it as a cloud storage.
I highlighted it for your convenience.

## FAQs

> You've just quoted their FAQs.

Yes I did.

Here is the link: [FAQs](http://pastebin.com/faq).

## Why Pastebin?

There is no particular reason for (at least not while I am writing this) using
Pastebin. You could also use [GitHub's Gists](https://gist.github.com) or some
similar service.

## Has someone done that before?

Honestly, I do not know.

## Is it allowed?

Quoted from their FAQs again:

> Please do NOT post:
> - email lists
> - login details
> - stolen source code
> - password lists
> - personal information / data
> - pornographic information / data
> - spam links (this includes promoting your own site)

I wrote them an email and they responded (surprisingly fast) that I was allowed
to do it.
They even wished me a happy coding.


# Problems

So, does all of this work?

Let's find out!

## Limitations

Of course they have some limitations. They are **not** stupid.

### Uploads

| Membership | pastes per 24 hours |
| :--------- | ------------------: |
| Guests     |    10               |
| Registered |    20               |
| Pro        |   250               |

### Type of Pastes

There are three different types of pastes:

- public
	- listed on their website
- unlisted
	- not listed on their website, only accessible via link
- private
	- only visible to you

#### Limits

| membership | public    | unlisted  | private        |
| :--------- | :-------: | :-------: | :------------: |
| Guest      | unlimited | unlimited | obviously none |
| Registered | unlimited | 25        | 10             |
| Pro        | unlimited | unlimited | unlimited      |

### Size Limit

Every post can be of _512 kilobytes_ in size.
Pro users have a limit of up to _10 megabytes_.

<!-- TODO: check if they mean powers of ten or two -->

### API

The API is only accessible for Registered or Pro users.

### Spamfilter

> Pastebin uses an automated spam protection system that will sometimes display
> a captcha request after you have tried to create a new paste. When you get a
> captcha request, you have 10 minutes to enter a valid response. If you don't
> validate your paste within 10 minutes, we will automatically remove it.
> 
> Various things can trigger this captcha spam protection.
> 
> A few examples are:
> - trying to create a certain amount of new pastes in a short period of time.
>   (flooding)
> - trying to create pastes with links in it.
> - trying to create pastes with 'suspicious' keywords in it.
> 
> There are various levels of spam protection. Anonymous guests, free members
> and PRO users all have different spam detection levels. Being a PRO member
> will allow you to post _almost_ anything without the automatic spam protection
> being activated.


# Are those really problems?

The number of pastes is irrelevant because we will post everything as a
encrypted public post.
We cannot use private or at least unlisted posts because we are no Pro user.
Well at least there might be people who are not and we want to take care of
everybody.
However, Guests have no API-access and Registered users are limited to public
posts, so we choose the registered one because we encrypt our data and also want
the higher upload limit.

The API is not a problem as we are Registered now.

## Size and Upload Limit

Below are some calculations for the upload volume of the different users.

### Registered

Registered users have _512 kilobytes_ times _20 per day_.
That get's us about **10 megabytes per day**.

### Pro

_10 megabytes_ (that is the whole upload of a registered user per day) times
_250_ equals **2500 megabytes** which is 20 gigabit or **2.5 gigabytes** per day.

## Spamfilter

The implementation of an automated captcha downloader which displays the picture
to you, or a simple notification asking you to visit the website and solve it.

A mechanism to spread the uploads over some time to not trigger captchas at all
might be useful.


# Format and Encryption

There are some things to consider:

## Limited Character Range

We could possibly use [base64](https://en.wikipedia.org/wiki/Base64) which comes
with a loss of **one third** of payload.

## Directory Structure and Filenames

### Fileheader vs. Linked List Index

#### Fileheader

- one post can be saved as a local file without lookup

#### Index

- single page acting as index
- long file or directory names
- changelog (restoring of previous versions)
- saving multiple files into one paste

## Compression

We already use base64 or something similar, why not compress our data to reduce
payload?

- gzip
- bzip2
	- good for text files
- xz
	- good for binary data

<!-- TODO: add more -->

## Encryption

This point is very obvious, as we do not want our data to be publicly readable.

- symmetric (AES)
	- fast
	- password can be lost
- asymmetric (RSA)
	- no human guessable password
	- keys need to be copied
	- signing possible

<!-- TODO: add more algorithms -->

A huge problem could be changing the password, if you have uploaded a lot.
This could be solved deleting all previous pastes and reuploading them newly
encrypted.

### Per File Encryption 

Theoretically aforementioned problem could be lessened by storing all
passwords/keys encrypted in a directory and use a master password.
So only the affected passwords/files need to be reuploaded.
The overall guessability of passwords, based on the knowledge of the unencrypted
contents of files, gets down to about zero.

