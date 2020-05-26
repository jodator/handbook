---
description: About the Joystream Handbook
---

# Introduction

### How To Contribute To The Joystream Handbook

We are using GitBook to organize the handbook.

If you would like to contribute to the handbook, simply fork this repo and make a pull request with your changes. Once merged into the `master` branch by a maintainer, your changes will be live [here](https://joystream.gitbook.io/joystream-handbook/).

### Formatting And Repo Structure

Adding a new guide section can be done by creating a markdown file in the section you want to add to (sections are represented as folders, which can also be added by simply creating the folder).

#### Summary Section

The summary file (SUMMARY.md) is a markdown file that should have the following structure:

```
# Summary

## Use headings to create page groups like this one​

* [First page's title](page1/README.md)    
    * [Some child page](page1/page1-1.md)    
    * [Some other child page](part1/page1-2.md)
    
* [Second page's title](page2/README.md)    
    * [Some child page](page2/page2-1.md)    
    * [Some other child page](part2/page2-2.md)    
    
## A second-page group​

* [Yet another page](another-page.md)
```

Providing a custom summary file is optional. 

By default, GitBook will look for a file named SUMMARY.md in your root folder if specified in your config file, or at the root of the repository otherwise.

If you don't specify a summary, and GitBook does not find a SUMMARY.md file at the root of your docs, GitBook will infer the table of contents from the folder structure and the Markdown files below.

#### Assets
To keep the repo clean, keep assets in this folder: `.gitbook/assets`.
