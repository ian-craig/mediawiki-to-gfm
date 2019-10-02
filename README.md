# Mediawiki to Github Flavoured Markdown

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

Convert a MediaWiki export to a directory of Markdown files for migration to Azure DevOps Wiki.

A fork of [outofcontrol/mediawiki-to-gfm](https://github.com/outofcontrol/mediawiki-to-gfm) with some additional tweaks to for migration to Azure DevOps Wiki.

## Dependencies

* PHP: Tested in PHP 7.0, 7.1, 7.2 and 7.3
* Pandoc: Installation instructions are here https://pandoc.org/installing.html
    - Tested on version 2.0.1.1, 2.0.2 and 2.7.3
* Composer: Installation instructions are here https://getcomposer.org/download/

## Installation 

- Ensure all dependencies are installed manually
- Clone the repo
- Run `composer update --no-dev` from the repo root

## Run

Run the script on your exported MediaWiki XML file:

    php ./convert.php --filename=/path/to/filename.xml --output=/path/to/converted/files 

## Options

    php ./convert.php --filename=/path/to/filename.xml --output=/path/to/converted/files --format=gfm --addmeta --flatten --indexes

    --filename : Location of the mediawiki exported XML file to convert 
                 to GFM format (Required)
    --output   : Location where you would like to save the converted files
                 (Default: ./output)
    --format   : What format would you like to convert to. Default is GFM 
                 (for use in Gitlab and Github) See pandoc documentation
                 for more formats (Default: 'gfm')
    --addmeta  : This flag will add a Permalink to each file (Default: false)
    --flatten  : This flag will force all pages to be saved in a single level 
                 directory. File names will be converted in the following way:
                 Mediawiki_folder/My_File_Name -> Mediawiki_folder_My_File_Name
                 and saved in a file called 'Mediawiki_folder_My_File_Name.md' 
                 (Default: false)
    --help     : This help message (almost)

## Export Mediawiki Files to XML 

In order to convert from MediaWiki format to GFM and use in Gitlab (or Github), you will first need to export all the pages you wish to convert from Mediawiki into an XML file. Here are a few simple steps to help
you accomplish this quickly:

1. MediaWiki -> Special Pages -> 'All Pages'
1. With help from the filter tool at the top of 'All Pages', copy the page names to convert into a text file (one file name per line).
1. MediaWiki -> Special Pages -> 'Export'
1. Paste the list of pages into the Export field. 
1. Check: 'Include only the current revision, not the full history'  
   Note: This convert script will only do latest version, not revisions. 
1. Uncheck: Include Templates
1. Check: Save as file
1. Click on the 'Export' button.
1. An XML file will be saved locally. 
1. Use this convert.php script to convert the XML file a set of GFM formatted pages. 

In theory you can convert to any of these formats… (not tested):  
    https://pandoc.org/MANUAL.html#description

Updates and improvements are welcome! Please only submit a PR if you have also written tests and tested your code! To run phpunit tests, update composer without the --no-dev parameter:

    composer update
