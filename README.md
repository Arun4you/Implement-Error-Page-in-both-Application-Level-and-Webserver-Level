# Implement-Error-Page-in-both-Application-Level-and-Webserver-Level
This document describes how to set up the Apache plug-in to return different error pages depending on the HTTP error.

This document describes how to set up the Apache plug-in to return different error pages depending on the HTTP error.
Fix

There are two ways to implement HTTP error messages: at the application or web server level.

1. Application Level

Set element error-page in the deployment descriptor (web.xml file). It specifies a mapping between an error code or exception type to the path of a resource in the Web application.

When an error occurs - while WebLogic Server is responding to an HTTP request, or as a result of a Java exception - WebLogic Server returns an HTML page that displays either the HTTP error code or a page containing the Java error message. You can define your own HTML page to be displayed in place of these default error pages or in response to a Java exception.

This is explained in the following documentation: Oracle® Fusion Middleware Developing Web Applications, Servlets, and JSPs for Oracle WebLogic Server.

2. Apache Level

There is a directive called ErrorDocument that should be set in the Apache configuration. If defines the web server response in case of an error. More details could be found in the Apache documentation.

Minimal httpd.conf example:
Listen 80

User apache
Group apache

ErrorLog /var/log/httpd/error_log

ErrorDocument 500 http://foo.example.com/cgi-bin/tester
ErrorDocument 404 /cgi-bin/bad_urls.pl
ErrorDocument 401 /info.html
ErrorDocument 403 "Sorry can't process your request. Try again later."
