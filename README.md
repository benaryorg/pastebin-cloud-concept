Using [Pastebin](http://pastebin.com) as a Cloud
================================================

# Pastebin

Quoted from their FAQs:

> Pastebin.com is a website where you can store text for a certain period of
> time. The website is mainly used by programmers to store pieces of sources
> code or configuration information, but anyone is more than welcome to paste
> any type of text. The idea behind the site is to make it more convenient for
> people to share large amounts of text online.

Here we have the main keyword which led me to the idea, more than once, to use
it as a cloud storage.

It is the keyword **_store_**.

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

So, you want to implement it?

Okay, first we try to find out if it is possible.

## Limitations

Of course they have some limitations. They are not stupid.

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

Every post can be of 512 kilobytes in size.
Pro users have a limit of up to 10 megabytes.

<!-- TODO: check if they mean powers of ten or two -->

### API

The API is only accessible for Registered or Pro users.

