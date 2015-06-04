Using [Pastebin](http://pastebin.com) as a Cloud
================================================


# Contribution

First of all, if you want to contribute, please send a pull request.

There are some TODOs as HTML comments in the text and here are some more:

- add italics and bold font where appropriate
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

So, from what I see, it could be allowed, as long as your personal information
is not personal, which could be solved using encryption.

<!-- TODO: check if it could really be done -->


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

