---
layout: lesson
root: .
title: Downloading Data
---

## Downloading Data
There are many resources and data files on the internet and while downloading data may be simply done with a mouse click on your own computer, this approach is useless when writing scripts or if the data is needed on a server.

> ## Prerequisites {.prereq}
> 
>Basic knowledge of the command line.
> 

## Learning Objectives 
In this lesson we will learn to download files using the command line.

## Lesson 
Downloading a file using the command line is pretty straightforward and in linux we have different options.

### _wget_
All that is needed is the URL to the file:
```
wget URL.of.file
```
This will download the file in the URL in the present working directory.
The process is non-interactive so you can logoff while the download goes on.

From the wget manpage:
> Wget is non-interactive, meaning that it can work in the background, while the user is not logged on.
>This allows you to start a retrieval and disconnect from the system, letting Wget finish the work. By contrast, most of the Web browsers require constant user's presence, which can be a great hindrance when transferring a lot of data.

Wget will resume stopped downloads by passing the -c flag.
```
wget -c http://link.to.partially.downloaded.file
```

Wget has many other options that are described in the manpage, some of notable use are:

* -b    (Go to background immediately after startup)
* -o _logfile_     (Log all messages to logfile, useful when running in the background or unattended)
* -c    (Continue getting a partially-downloaded file)
* --user=user; --password=password (Specify the username user and password password for FTP/HTTP file retrieval)

### curl
Curl works just like wget and the syntax is similar:
```
curl URL.of.partial.file
```
As always refer to the man page for the various options and flags available; curl will try to resume a partial download when using -C  - (there is a space and a dash (-) after the flag)
```
curl -C - URL.of.partial.file
```
Other flags of note:

* -u user:password  (Specify  username and password to use for server authentication)
* -C  -    (Try to resume a download)


### rsync
Rsync is a fast tool that copies files over a secure shell connection, as such it can be used to copy files(and directories) to and from any machine that you have access to.
Since it computes the differences between the source and destination, it reduces the  amount  of data sent over the network by sending only the differences.

The usual large array of option are best described in the man page, we will only concentrate on basic file copying. 

To copy a file from the remote server (HOST) in which you are logged in as USER:
```
rsync USER@HOST:/path/to/file /local/destination
```
To copy a file to the remote server HOST where you have access as USER:
```
rsync /path/to/local/file   USER@HOST:/remote/destination/
```

The transfers will be run over ssh, so you will be asked to authenticate.
 

> ### Exercise
> Download a file from the command line using wget and curl.
> 
