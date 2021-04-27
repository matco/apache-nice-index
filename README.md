# Apache nice index
This project contains the files required to enhance the automatic file listing (named `autoindex`) provided by the Apache web server.

## Setup

### Enable nice index
First, checkout this project somewhere, for example `/opt/apache-nice-index`.

Then, enable the modules `alias` and `autoindex` in Apache. Find the line for these modules in your Apache configuration and uncomment them if required:
```
LoadModule alias_module modules/mod_alias.so
LoadModule autoindex_module modules/mod_autoindex.so
```

Then, include the custom Apache configuration of the project in your main Apache configuration:
```
Include "/opt/apache-nice-index/apache.conf
```
The custom configuration does the following things:
* Serve the folder `www` of the project by Apache at `/autoindex`
* Enable custom autoindex configuration

If you would like to checkout the project in a different folder than `/opt/apache-nice-index`, you will need to update the file `apache.conf` with your own path.

If you would like to choose a different alias than `/autoindex`, you will need to update the files `apache.conf` and `header.html` with your own alias.

### Enable autoindex for your directories
Once the setup is done, you need to enable autoindex for the directories of your choice. You can add the configuration directly in the main Apache configuration or in a `.htaccess` file directly in the folder to index. Just add `Options +Indexes` inside your `Directory` tag.

To allow autoindex for all the directories served by Apache, use:
```
<Directory />
	Options +Indexes
</Directory>
```

You can customize the autoindex options using the `IndexOptions` parameter. The more interesting option is the style of the index, to be chosen among `HTMLTable` (display files in an HTML table), `FancyIndexing` (use a well-indented block of text) or nothing (display files in an HTML list). The default is `HTMLTable`. For example:
```
<Directory />
	Options +Indexes
	IndexOptions FancyIndexing
</Directory>
```

You can check the Apache documentation [here](https://httpd.apache.org/docs/2.4/mod/mod_autoindex.html#indexoptions) to discover the available options.
