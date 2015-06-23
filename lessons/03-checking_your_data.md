---
layout: lesson
root: .
title: Verifying Data
---

Data that is generated needs to be shared, but sharing a corrupted dataset can be potentially time-wasting for the end-user. We need to ensure that the file that is downloaded is consistent with the original.


> ## Prerequisites {.prereq}
>
> Only basic knowledge of the command line is needed.
>You must have the md5sum program (for Unix) or the equivalent File Checksum Integrity Verifier (for Windows)

## Learning Objectives 
In this lesson we will see how to check the files we have downloaded using an MD5 consistency check.


## Lesson 
The MD5 algorithm is a function that produces a hash value typically expressed in text format as a 32 digit hexadecimal number. MD5 hash values have been widely used to ensure that file transfers have completed successfully; in the unix world most distibutions come with the md5sum program installed, windows users must rely on specific utilities (see this [Microsoft Knowledge base article](https://support.microsoft.com/en-us/kb/841290)).
 
### Computing the MD5 value
Given a file the MD5 value can be computed simply by passing the file to the md5sum function

```
md5sum DataFileToCheck
```

An example (depending on the contents of the file) output would be:
```
adf6aa82f348ef7553c8c6fed5cf3c33  DataFileToCheck
```

This output is usually piped to a file named MD5SUMS that is then placed alongside the datafile.

```
md5sum DataFileToCheck > MD5SUMS
```

For Windows users the command is similar:
```
fciv.exe -md5 DataFileToCheck -xml MD5SUMS.xml
```

### Verifying a file with the MD5 hash
To verify the downloaded file, we also download the MD5SUMS file and run md5sum with the -c flag and the file containing the hash. We must run this in the same directory of the downloaded file.

> 
>md5sum -c MD5SUMS
> 
 
The expected output is a line as follows:

> datafile: OK

The equivalent Windows command is:
```
fciv.exe -v DataFileToCheck -md5 -xml MD5SUMS.xml
```


> ### Exercise
> Download the sample file ([datafile](../../../../data-genomics/blob/gh-pages/datafile)) and its MD5SUMS ([MD5SUMS](../../../../data-genomics/blob/gh-pages/MD5SUMS)) file.
> 
> Verify the file using the md5sum command.
>  
> Now change the content of the sample file and verify it again.
> 

## Conclusions
A single change to the file will make the md5sum check fail, this could be caused by altered data or by errors during the transfer process. This quick and simple check can save time later, allowing you to exclude the possibiliy of a corrupted dataset.
This can also come in handy after a crash to check if the file has been corrupted.
