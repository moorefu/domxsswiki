#sidebar SideBarMenu
= Table of Contents =
<wiki:toc max_depth="3" />
= Introduction =

DOM Xss Test Cases Wiki Project

= Details =

== Sources ==

=== How to read tables ===
Tables contents describe output given some input.
Headers are:

 * *source*: Javascript object name
 * *browser*: Browser Name
 * *version*: Browser version tested
 * *pathInfo*: characters that are not urlencoded in the pathInfo part
 * *Search*: characters that are not urlencoded in the search part
 * *Hash*:  characters that are not urlencoded in the hash part
 * *output sample*: A sample of the output given by getting the property, if needed.

Sometimes you'll find something like `[`A-B`]`, that means that it has to be considered the whole interval of ascii characters from A to B.

The missing characters in the table elements are to be considered urlencoded, if described otherwise and excluding */`[`a-z0-9`]`/i*

Finally, some interesting characters are bold.

=== The location/documentURI/URL Sources ===

Considering the classic url format:

*scheme://user:pass@host/path/to/page.ext/<font color="red">Pathinfo;semicolon</font><font color="green">?search.location=value</font><font color="blue">#hash=value&hash2=value2</font>*

and given a sample url:

*http://host/path/to/page.ext/<font color="red">test<a"'%0A```= +%20>;test<a"'%0A```= +%20></font><font color="green">?test<a"'%0A```= +%20>;</font><font color="blue">#test<a"'%0A```= +%20>;*</font>

the following table shows how direct call of
 * document.URL
 * document.documentURI
 * document.URLUnencoded (IE 5.5 or later Only)
 * document.baseURI
 * location
 * location.href
 * location.search
 * location.hash
 * location.pathname

are natively treated:


|| *Source* || *browser* || *version* || *pathInfo* || *Search* || *Hash* || *output sample*||
|| document.URL ||   IE 8     ||  8       || 33 (`!`), 36 (`$`), 38 (`&`), 39 (`'`), 40 (`(`), 41 (`)`), 42 (`*`), 43 (`+`), 44 (`,`), 45 (`-`), 46 (`.`), 47 (`/`), 58 (`:`), 59 (`;`), 61 (`=`), 64 (`@`), 91 (`[`), 93 (`]`), 95 (`_`), 126 (`~`), `[`128-255`]` || 1, 2, 3, 4, 5, 6, 7, 8, 11, 12, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24, 25, 26, 27, 28, 29, 30, 31, 32 (` `), 33 (`!`), 34 (`"`), 36 (`$`), 38 (`&`), 39 (`'`), 40 (`(`), 41 (`)`), 42 (`*`), 43 (`+`), 44 (`,`), 45 (`-`), 46 (`.`), 47 (`/`), 58 (`:`), 59 (`;`), 60 (`<`), 61 (`=`), 62 (`>`), 63 (`?`), 64 (`@`), 91 (`[`), 92 (`\`), 93 (`]`), 94 (`^`), 95 (`_`), 96 (```), 123 (`{`), 124 (`|`), 125 (`}`), 126 (`~`), `[`127-255`]`  || 1, 2, 3, 4, 5, 6, 7, 8, 11, 12, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24, 25, 26, 27, 28, 29, 30, 31, 32 (` `), 33 (`!`), 34 (`"`), 35 (`#`), 36 (`$`), 38 (`&`), 39 (`'`), 40 (`(`), 41 (`)`), 42 (`*`), 43 (`+`), 44 (`,`), 45 (`-`), 46 (`.`), 47 (`/`), 58 (`:`), 59 (`;`), 60 (`<`), 61 (`=`), 62 (`>`), 63 (`?`), 64 (`@`), 91 (`[`), 92 (`\`), 93 (`]`), 94 (`^`), 95 (`_`), 96 (```), 123 (`{`), 124 (`|`), 125 (`}`), 126 (`~`), `[`127 - 255`]`  ||  http://host/path/to/page.ext/<font color="red">test%3Ca%22'%0A%60=%20+%20%3E;test%3Ca%22'%0A%60=%20+%20%3E</font><font color="green">?test<a"'%0A```=%20+%20>;<font color="blue">#test<a"'%0A```=%20+%20>;</font>||
|| document.URL ||    Firefox     ||  3.6.8     || 33 (`!`), 36 (`$`), 37 (`%`), 38 (`&`), 40 (`(`), 41 (`)`), 42 (`*`), 43 (`+`), 44 (`,`), 45 (`-`), 46 (`.`), 47 (`/`), 58 (`:`), 59 (`;`), 61 (`=`), 63 (`?`), 64 (`@`), 91 (`[`), 92 (`\`), 93 (`]`), 94 (`^`), 95 (`_`), 123 (`{`), 124 (`|`), 125 (`}`), 126 (`~`)  || 33 (`!`), 36 (`$`), 37 (`%`), 38 (`&`), 40 (`(`), 41 (`)`), 42 (`*`), 43 (`+`), 44 (`,`), 45 (`-`), 46 (`.`), 47 (`/`), 58 (`:`), 59 (`;`), 61 (`=`), 63 (`?`), 64 (`@`), 91 (`[`), 92 (`\`), 93 (`]`), 94 (`^`), 95 (`_`), 123 (`{`), 124 (`|`), 125 (`}`), 126 (`~`)  || 33 (`!`), 35 (`#`), 36 (`$`), 37 (`%`), 38 (`&`), 40 (`(`), 41 (`)`), 42 (`*`), 43 (`+`), 44 (`,`), 45 (`-`), 46 (`.`), 47 (`/`), 58 (`:`), 59 (`;`), 61 (`=`), 63 (`?`), 64 (`@`), 91 (`[`), 92 (`\`), 93 (`]`), 94 (`^`), 95 (`_`), 123 (`{`), 124 (`|`), 125 (`}`), 126 (`~`)  || http://host/path/to/page.ext/<font color="red">test%3Ca%22%27%0A%60=%20+%20%3E;test%3Ca%22%27%0A%60=%20+%20%3E</font><font color="green">?test%3Ca%22%27%0A%60=%20+%20%3E;<font color="blue">#test%3Ca%22%27%0A%60=%20+%20%3E;</font>    ||
|| document.URL ||   Chrome     ||   6.0.472.53 beta     ||  33 (`!`), 36 (`$`), 37 (`%`), 38 (`&`), 39 (`'`), 40 (`(`), 41 (`)`), 42 (`*`), 43 (`+`), 44 (`,`), 45 (`-`), 46 (`.`), 47 (`/`), 58 (`:`), 59 (`;`), 61 (`=`), 64 (`@`), 91 (`[`), 93 (`]`), 95 (`_`), 126 (`~`) || 33 (`!`), 36 (`$`), 37 (`%`), 38 (`&`), 39 (`'`), 40 (`(`), 41 (`)`), 42 (`*`), 43 (`+`), 44 (`,`), 45 (`-`), 46 (`.`), 47 (`/`), 58 (`:`), 59 (`;`), 61 (`=`), 63 (`?`), 64 (`@`), 91 (`[`), 92 (`\`), 93 (`]`), 94 (`^`), 95 (`_`), 96 (```), 123 (`{`), 124 (`|`), 125 (`}`), 126 (`~`) || 32 (` `), 33 (`!`), 34 (`"`), 35 (`#`), 36 (`$`), 37 (`%`), 38 (`&`), 39 (`'`), 40 (`(`), 41 (`)`), 42 (`*`), 43 (`+`), 44 (`,`), 45 (`-`), 46 (`.`), 47 (`/`), 58 (`:`), 59 (`;`), 60 (`<`), 61 (`=`), 62 (`>`), 63 (`?`), 64 (`@`), 91 (`[`), 92 (`\`), 93 (`]`), 94 (`^`), 95 (`_`), 96 (```), 123 (`{`), 124 (`|`), 125 (`}`), 126 (`~`), `[`127 - 255`]`  || http://host/path/to/page.ext/<font color="red">test%3Ca%22'%0A%60=%20+%20%3E;test%3Ca%22'%0A%60=%20+%20%3E</font><font color="green">?test%3Ca%22'%0A```=%20+%20%3E;<font color="blue">#test<a"'%0A```= +%20>;</font>     ||
|| document.URL ||    Opera     ||  10.61     || 33 (`!`), 36 (`$`), 37 (`%`), 38 (`&`), 39 (`'`), 40 (`(`), 41 (`)`), 42 (`*`), 43 (`+`), 44 (`,`), 45 (`-`), 46 (`.`), 47 (`/`), 58 (`:`), 59 (`;`), 61 (`=`), 64 (`@`), 91 (`[`), 93 (`]`), 94 (`^`), 95 (`_`), 96 (```), 123 (`{`), 124 (`|`), 125 (`}`), 126 (`~`), `[`127 - 255`]`  || 33 (`!`), 36 (`$`), 37 (`%`), 38 (`&`), 39 (`'`), 40 (`(`), 41 (`)`), 42 (`*`), 43 (`+`), 44 (`,`), 45 (`-`), 46 (`.`), 47 (`/`), 58 (`:`), 59 (`;`), 61 (`=`), 63 (`?`), 64 (`@`), 91 (`[`), 93 (`]`), 94 (`^`), 95 (`_`), 123 (`{`), 124 (`|`), 125 (`}`), 126 (`~`)  || 33 (`!`), 35 (`#`), 36 (`$`), 37 (`%`), 38 (`&`), 39 (`'`), 40 (`(`), 41 (`)`), 42 (`*`), 43 (`+`), 44 (`,`), 45 (`-`), 46 (`.`), 47 (`/`), 58 (`:`), 59 (`;`), 61 (`=`), 64 (`@`), 91 (`[`), 93 (`]`), 94 (`^`), 95 (`_`), 96 (```), 123 (`{`), 124 (`|`), 125 (`}`), 126 (`~`), `[`127 - 255`]` || http://host/path/to/page.ext/<font color="red">test%3Ca%22'%0A```=%20+%20%3E;test%3Ca%22'%0A```=%20+%20%3E</font><font color="green">?test%3Ca%22'%0A%60=%20+%20%3E;<font color="blue">#test<a"'%0A```= +%20>;</font>    ||
|| document.documentURI ||   IE 8     ||  8       ||  undefined  || undefined ||undefined  ||  undefined     ||
|| document.documentURI ||    Firefox     ||  3.6.8        || 33 (`!`), 36 (`$`), 37 (`%`), 38 (`&`), 40 (`(`), 41 (`)`), 42 (`*`), 43 (`+`), 44 (`,`), 45 (`-`), 46 (`.`), 47 (`/`), 58 (`:`), 59 (`;`), 61 (`=`), 64 (`@`), 91 (`[`), 92 (`\`), 93 (`]`), 94 (`^`), 95 (`_`), 123 (`{`), 124 (`|`), 125 (`}`), 126 (`~`)  || 33 (`!`), 36 (`$`), 37 (`%`), 38 (`&`), 40 (`(`), 41 (`)`), 42 (`*`), 43 (`+`), 44 (`,`), 45 (`-`), 46 (`.`), 47 (`/`), 58 (`:`), 59 (`;`), 61 (`=`), 63 (`?`), 64 (`@`), 91 (`[`), 92 (`\`), 93 (`]`), 94 (`^`), 95 (`_`), 123 (`{`), 124 (`|`), 125 (`}`), 126 (`~`)  ||  33 (`!`), 35 (`#`), 36 (`$`), 37 (`%`), 38 (`&`), 40 (`(`), 41 (`)`), 42 (`*`), 43 (`+`), 44 (`,`), 45 (`-`), 46 (`.`), 47 (`/`), 58 (`:`), 59 (`;`), 61 (`=`), 63 (`?`), 64 (`@`), 91 (`[`), 92 (`\`), 93 (`]`), 94 (`^`), 95 (`_`), 123 (`{`), 124 (`|`), 125 (`}`), 126 (`~`) ||   http://host/path/to/page.ext/<font color="red">test%3Ca%22%27%0A%60=%20+%20%3E;test%3Ca%22%27%0A%60=%20+%20%3E</font><font color="green">?test%3Ca%22%27%0A%60=%20+%20%3E;<font color="blue">#test%3Ca%22%27%0A%60=%20+%20%3E;</font>     ||
|| document.documentURI ||    Chrome     ||   6.0.472.53 beta  || 33 (`!`), 36 (`$`), 37 (`%`), 38 (`&`), 39 (`'`), 40 (`(`), 41 (`)`), 42 (`*`), 43 (`+`), 44 (`,`), 45 (`-`), 46 (`.`), 47 (`/`), 58 (`:`), 59 (`;`), 61 (`=`), 64 (`@`), 91 (`[`), 93 (`]`), 95 (`_`), 126 (`~`)  || 33 (`!`), 36 (`$`), 37 (`%`), 38 (`&`), 39 (`'`), 40 (`(`), 41 (`)`), 42 (`*`), 43 (`+`), 44 (`,`), 45 (`-`), 46 (`.`), 47 (`/`), 58 (`:`), 59 (`;`), 61 (`=`), 63 (`?`), 64 (`@`), 91 (`[`), 92 (`\`), 93 (`]`), 94 (`^`), 95 (`_`), 96 (```), 123 (`{`), 124 (`|`), 125 (`}`), 126 (`~`) || 32 (` `), 33 (`!`), 34 (`"`), 35 (`#`), 36 (`$`), 37 (`%`), 38 (`&`), 39 (`'`), 40 (`(`), 41 (`)`), 42 (`*`), 43 (`+`), 44 (`,`), 45 (`-`), 46 (`.`), 47 (`/`), 58 (`:`), 59 (`;`), 60 (`<`), 61 (`=`), 62 (`>`), 63 (`?`), 64 (`@`), 91 (`[`), 92 (`\`), 93 (`]`), 94 (`^`), 95 (`_`), 96 (```), 123 (`{`), 124 (`|`), 125 (`}`), 126 (`~`),  `[`127 - 255`]` ||    http://host/path/to/page.ext/<font color="red">test%3Ca%22'%0A%60=%20+%20%3E;test%3Ca%22'%0A%60=%20+%20%3E</font><font color="green">?test%3Ca%22'%0A```=%20+%20%3E;<font color="blue">#test<a"'%0A```= +%20>;</font>     ||
|| document.documentURI ||    Opera     ||  10.61        || 255, 33 (`!`), 36 (`$`), 37 (`%`), 38 (`&`), 39 (`'`), 40 (`(`), 41 (`)`), 42 (`*`), 43 (`+`), 44 (`,`), 45 (`-`), 46 (`.`), 47 (`/`), 58 (`:`), 59 (`;`), 61 (`=`), 64 (`@`), 91 (`[`), 93 (`]`), 94 (`^`), 95 (`_`), 96 (```), 123 (`{`), 124 (`|`), 125 (`}`), 126 (`~`), `[`127 - 255`]` || 33 (`!`), 36 (`$`), 37 (`%`), 38 (`&`), 39 (`'`), 40 (`(`), 41 (`)`), 42 (`*`), 43 (`+`), 44 (`,`), 45 (`-`), 46 (`.`), 47 (`/`), 58 (`:`), 59 (`;`), 61 (`=`), 63 (`?`), 64 (`@`), 91 (`[`), 93 (`]`), 94 (`^`), 95 (`_`), 123 (`{`), 124 (`|`), 125 (`}`), 126 (`~`)  || *No Hash* ||    http://host/path/to/page.ext/<font color="red">test%3Ca%22'%0A```=%20+%20%3E;test%3Ca%22'%0A```=%20+%20%3E</font><font color="green">?test%3Ca%22'%0A%60=%20+%20%3E;</font>     ||
|| document.URLUnencoded ||   IE 8     ||  8       ||  33 (`!`), 36 (`$`), 38 (`&`), 39 (`'`), 40 (`(`), 41 (`)`), 42 (`*`), 43 (`+`), 44 (`,`), 45 (`-`), 46 (`.`), 47 (`/`), 58 (`:`), 59 (`;`), 61 (`=`), 64 (`@`), 91 (`[`), 93 (`]`), 95 (`_`), 126 (`~`), `[`128 - 255`]`  || 1, 2, 3, 4, 5, 6, 7, 8, 11, 12, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24, 25, 26, 27, 28, 29, 30, 31, 32 (` `), 33 (`!`), 34 (`"`), 36 (`$`), 38 (`&`), 39 (`'`), 40 (`(`), 41 (`)`), 42 (`*`), 43 (`+`), 44 (`,`), 45 (`-`), 46 (`.`), 47 (`/`), 58 (`:`), 59 (`;`), 60 (`<`), 61 (`=`), 62 (`>`), 63 (`?`), 64 (`@`), 91 (`[`), 92 (`\`), 93 (`]`), 94 (`^`), 95 (`_`), 96 (```), 123 (`{`), 124 (`|`), 125 (`}`), 126 (`~`), `[`127 - 255`]` || 1, 2, 3, 4, 5, 6, 7, 8, 11, 12, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24, 25, 26, 27, 28, 29, 30, 31, 32 (` `), 33 (`!`), 34 (`"`), 35 (`#`), 36 (`$`), 38 (`&`), 39 (`'`), 40 (`(`), 41 (`)`), 42 (`*`), 43 (`+`), 44 (`,`), 45 (`-`), 46 (`.`), 47 (`/`), 58 (`:`), 59 (`;`), 60 (`<`), 61 (`=`), 62 (`>`), 63 (`?`), 64 (`@`), 91 (`[`), 92 (`\`), 93 (`]`), 94 (`^`), 95 (`_`), 96 (```), 123 (`{`), 124 (`|`), 125 (`}`), 126 (`~`), `[`127 - 255`]`  ||   http://host/path/to/page.ext/<font color="red">test%3Ca%22'%0A%60=%20+%20%3E;test%3Ca%22'%0A%60=%20+%20%3E</font><font color="green">?test<a"'%0A```=%20+%20>;<font color="blue">#test<a"'%0A```=%20+%20>;</font>  ||
|| document.URLUnencoded ||   Firefox     ||  3.6.8         ||  undefined || undefined  || undefined || undefined    ||
|| document.URLUnencoded ||     Chrome     ||   6.0.472.53 beta     ||  undefined ||  undefined || undefined ||  undefined    ||
|| document.URLUnencoded ||   Opera     ||  10.61         || undefined  || undefined  || undefined  || undefined    ||
|| document.baseURI ||   IE 8     ||  8       || undefined  || undefined || undefined ||    undefined     ||
|| document.baseURI ||     Firefox     ||  3.6.8         || 33 (`!`), 36 (`$`), 37 (`%`), 38 (`&`), 40 (`(`), 41 (`)`), 42 (`*`), 43 (`+`), 44 (`,`), 45 (`-`), 46 (`.`), 47 (`/`), 58 (`:`), 59 (`;`), 61 (`=`), 64 (`@`), 91 (`[`), 92 (`\`), 93 (`]`), 94 (`^`), 95 (`_`), 123 (`{`), 124 (`|`), 125 (`}`), 126 (`~`)  || 33 (`!`), 36 (`$`), 37 (`%`), 38 (`&`), 40 (`(`), 41 (`)`), 42 (`*`), 43 (`+`), 44 (`,`), 45 (`-`), 46 (`.`), 47 (`/`), 58 (`:`), 59 (`;`), 61 (`=`), 63 (`?`), 64 (`@`), 91 (`[`), 92 (`\`), 93 (`]`), 94 (`^`), 95 (`_`), 123 (`{`), 124 (`|`), 125 (`}`), 126 (`~`)  || 33 (`!`), 35 (`#`), 36 (`$`), 37 (`%`), 38 (`&`), 40 (`(`), 41 (`)`), 42 (`*`), 43 (`+`), 44 (`,`), 45 (`-`), 46 (`.`), 47 (`/`), 58 (`:`), 59 (`;`), 61 (`=`), 63 (`?`), 64 (`@`), 91 (`[`), 92 (`\`), 93 (`]`), 94 (`^`), 95 (`_`), 123 (`{`), 124 (`|`), 125 (`}`), 126 (`~`)  ||    http://host/path/to/page.ext/<font color="red">test%3Ca%22%27%0A%60=%20+%20%3E;test%3Ca%22%27%0A%60=%20+%20%3E</font><font color="green">?test%3Ca%22%27%0A%60=%20+%20%3E;<font color="blue">#test%3Ca%22%27%0A%60=%20+%20%3E;</font>    ||
|| document.baseURI ||      Chrome     ||   6.0.472.53 beta       || 33 (`!`), 36 (`$`), 37 (`%`), 38 (`&`), 39 (`'`), 40 (`(`), 41 (`)`), 42 (`*`), 43 (`+`), 44 (`,`), 45 (`-`), 46 (`.`), 47 (`/`), 58 (`:`), 59 (`;`), 61 (`=`), 64 (`@`), 91 (`[`), 93 (`]`), 95 (`_`), 126 (`~`) ||  33 (`!`), 36 (`$`), 37 (`%`), 38 (`&`), 39 (`'`), 40 (`(`), 41 (`)`), 42 (`*`), 43 (`+`), 44 (`,`), 45 (`-`), 46 (`.`), 47 (`/`), 58 (`:`), 59 (`;`), 61 (`=`), 63 (`?`), 64 (`@`), 91 (`[`), 92 (`\`), 93 (`]`), 94 (`^`), 95 (`_`), 96 (```), 123 (`{`), 124 (`|`), 125 (`}`), 126 (`~`) || 32 (` `), 33 (`!`), 34 (`"`), 35 (`#`), 36 (`$`), 37 (`%`), 38 (`&`), 39 (`'`), 40 (`(`), 41 (`)`), 42 (`*`), 43 (`+`), 44 (`,`), 45 (`-`), 46 (`.`), 47 (`/`), 58 (`:`), 59 (`;`), 60 (`<`), 61 (`=`), 62 (`>`), 63 (`?`), 64 (`@`), 91 (`[`), 92 (`\`), 93 (`]`), 94 (`^`), 95 (`_`), 96 (```), 123 (`{`), 124 (`|`), 125 (`}`), 126 (`~`), `[`127 - 255`]` ||    http://host/path/to/page.ext/<font color="red">test%3Ca%22'%0A%60=%20+%20%3E;test%3Ca%22'%0A%60=%20+%20%3E</font><font color="green">?test%3Ca%22'%0A```=%20+%20%3E;<font color="blue">#test<a"'%0A```= +%20>;</font>   ||
|| document.baseURI ||     Opera     ||  10.61         || 33 (`!`), 36 (`$`), 37 (`%`), 38 (`&`), 39 (`'`), 40 (`(`), 41 (`)`), 42 (`*`), 43 (`+`), 44 (`,`), 45 (`-`), 46 (`.`), 47 (`/`), 58 (`:`), 59 (`;`), 61 (`=`), 64 (`@`), 91 (`[`), 93 (`]`), 94 (`^`), 95 (`_`), 96 (```), 123 (`{`), 124 (`|`), 125 (`}`), 126 (`~`), `[`127 - 255`]`  || 33 (`!`), 36 (`$`), 37 (`%`), 38 (`&`), 39 (`'`), 40 (`(`), 41 (`)`), 42 (`*`), 43 (`+`), 44 (`,`), 45 (`-`), 46 (`.`), 47 (`/`), 58 (`:`), 59 (`;`), 61 (`=`), 63 (`?`), 64 (`@`), 91 (`[`), 93 (`]`), 94 (`^`), 95 (`_`), 123 (`{`), 124 (`|`), 125 (`}`), 126 (`~`) || *No Hash* ||    http://host/path/to/page.ext/<font color="red">test%3Ca%22'%0A```=%20+%20%3E;test%3Ca%22'%0A```=%20+%20%3E</font><font color="green">?test%3Ca%22'%0A%60=%20+%20%3E;</font>    ||
|| location ||   IE 8     ||  8       || 33 (`!`), 36 (`$`), 38 (`&`), 39 (`'`), 40 (`(`), 41 (`)`), 42 (`*`), 43 (`+`), 44 (`,`), 45 (`-`), 46 (`.`), 47 (`/`), 58 (`:`), 59 (`;`), 61 (`=`), 64 (`@`), 91 (`[`), 93 (`]`), 95 (`_`), 126 (`~`), `[`128 - 255`]`    ||  1, 2, 3, 4, 5, 6, 7, 8, 11, 12, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24, 25, 26, 27, 28, 29, 30, 31, 32 (` `), 33 (`!`), 34 (`"`), 36 (`$`), 38 (`&`), 39 (`'`), 40 (`(`), 41 (`)`), 42 (`*`), 43 (`+`), 44 (`,`), 45 (`-`), 46 (`.`), 47 (`/`), 58 (`:`), 59 (`;`), 60 (`<`), 61 (`=`), 62 (`>`), 63 (`?`), 64 (`@`), 91 (`[`), 92 (`\`), 93 (`]`), 94 (`^`), 95 (`_`), 96 (```), 123 (`{`), 124 (`|`), 125 (`}`), 126 (`~`), `[`127 -  255`]` ||  1, 2, 3, 4, 5, 6, 7, 8, 11, 12, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24, 25, 26, 27, 28, 29, 30, 31, 32 (` `), 33 (`!`), 34 (`"`), 35 (`#`), 36 (`$`), 38 (`&`), 39 (`'`), 40 (`(`), 41 (`)`), 42 (`*`), 43 (`+`), 44 (`,`), 45 (`-`), 46 (`.`), 47 (`/`), 58 (`:`), 59 (`;`), 60 (`<`), 61 (`=`), 62 (`>`), 63 (`?`), 64 (`@`), 91 (`[`), 92 (`\`), 93 (`]`), 94 (`^`), 95 (`_`), 96 (```), 123 (`{`), 124 (`|`), 125 (`}`), 126 (`~`), `[`127 - 255`]` ||  http://host/path/to/page.ext/<font color="red">test%3Ca%22'%0A%60=%20+%20%3E;test%3Ca%22'%0A%60=%20+%20%3E</font><font color="green">?test<a"'%0A```=%20+%20>;</font><font color="blue">#test<a"'%0A```=%20+%20>;</font>     ||
|| location ||   Firefox     ||  3.6.8      || 33 (`!`), 36 (`$`), 37 (`%`), 38 (`&`), 40 (`(`), 41 (`)`), 42 (`*`), 43 (`+`), 44 (`,`), 45 (`-`), 46 (`.`), 47 (`/`), 58 (`:`), 59 (`;`), 61 (`=`), 64 (`@`), 91 (`[`), 92 (`\`), 93 (`]`), 94 (`^`), 95 (`_`), 123 (`{`), 124 (`|`), 125 (`}`), 126 (`~`)  || 33 (`!`), 36 (`$`), 37 (`%`), 38 (`&`), 40 (`(`), 41 (`)`), 42 (`*`), 43 (`+`), 44 (`,`), 45 (`-`), 46 (`.`), 47 (`/`), 58 (`:`), 59 (`;`), 61 (`=`), 63 (`?`), 64 (`@`), 91 (`[`), 92 (`\`), 93 (`]`), 94 (`^`), 95 (`_`), 123 (`{`), 124 (`|`), 125 (`}`), 126 (`~`)  || 33 (`!`), 35 (`#`), 36 (`$`), 37 (`%`), 38 (`&`), 40 (`(`), 41 (`)`), 42 (`*`), 43 (`+`), 44 (`,`), 45 (`-`), 46 (`.`), 47 (`/`), 58 (`:`), 59 (`;`), 61 (`=`), 63 (`?`), 64 (`@`), 91 (`[`), 92 (`\`), 93 (`]`), 94 (`^`), 95 (`_`), 123 (`{`), 124 (`|`), 125 (`}`), 126 (`~`)  ||    http://host/path/to/page.ext/<font color="red">test%3Ca%22%27%0A%60=%20+%20%3E;test%3Ca%22%27%0A%60=%20+%20%3E</font><font color="green">?test%3Ca%22%27%0A%60=%20+%20%3E;</font><font color="blue">#test%3Ca%22%27%0A%60=%20+%20%3E;</font>    ||
|| location ||   Chrome     ||   6.0.472.53 beta     || 33 (`!`), 36 (`$`), 37 (`%`), 38 (`&`), 39 (`'`), 40 (`(`), 41 (`)`), 42 (`*`), 43 (`+`), 44 (`,`), 45 (`-`), 46 (`.`), 47 (`/`), 58 (`:`), 59 (`;`), 61 (`=`), 64 (`@`), 91 (`[`), 93 (`]`), 95 (`_`), 126 (`~`)   || 33 (`!`), 36 (`$`), 37 (`%`), 38 (`&`), 39 (`'`), 40 (`(`), 41 (`)`), 42 (`*`), 43 (`+`), 44 (`,`), 45 (`-`), 46 (`.`), 47 (`/`), 58 (`:`), 59 (`;`), 61 (`=`), 63 (`?`), 64 (`@`), 91 (`[`), 92 (`\`), 93 (`]`), 94 (`^`), 95 (`_`), 96 (```), 123 (`{`), 124 (`|`), 125 (`}`), 126 (`~`)  || 32 (` `), 33 (`!`), 34 (`"`), 35 (`#`), 36 (`$`), 37 (`%`), 38 (`&`), 39 (`'`), 40 (`(`), 41 (`)`), 42 (`*`), 43 (`+`), 44 (`,`), 45 (`-`), 46 (`.`), 47 (`/`), 58 (`:`), 59 (`;`), 60 (`<`), 61 (`=`), 62 (`>`), 63 (`?`), 64 (`@`), 91 (`[`), 92 (`\`), 93 (`]`), 94 (`^`), 95 (`_`), 96 (```), 123 (`{`), 124 (`|`), 125 (`}`), 126 (`~`), `[`127 -  255`]`  ||   http://host/path/to/page.ext/<font color="red">test%3Ca%22'%0A%60=%20+%20%3E;test%3Ca%22'%0A%60=%20+%20%3E</font><font color="green">?test%3Ca%22'%0A```=%20+%20%3E;</font><font color="blue">#test<a"'%0A```= +%20>;</font>    ||
|| location ||   Opera     ||  10.61       || 33 (`!`), 36 (`$`), 37 (`%`), 38 (`&`), 39 (`'`), 40 (`(`), 41 (`)`), 42 (`*`), 43 (`+`), 44 (`,`), 45 (`-`), 46 (`.`), 47 (`/`), 58 (`:`), 59 (`;`), 61 (`=`), 64 (`@`), 91 (`[`), 93 (`]`), 94 (`^`), 95 (`_`), 123 (`{`), 124 (`|`), 125 (`}`), 126 (`~`)   || 33 (`!`), 36 (`$`), 37 (`%`), 38 (`&`), 39 (`'`), 40 (`(`), 41 (`)`), 42 (`*`), 43 (`+`), 44 (`,`), 45 (`-`), 46 (`.`), 47 (`/`), 58 (`:`), 59 (`;`), 61 (`=`), 63 (`?`), 64 (`@`), 91 (`[`), 93 (`]`), 94 (`^`), 95 (`_`), 123 (`{`), 124 (`|`), 125 (`}`), 126 (`~`)  || 1, 2, 3, 4, 5, 6, 7, 8, 11, 12, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24, 25, 26, 27, 28, 29, 30, 31, 32 (` `), 33 (`!`), 34 (`"`), 35 (`#`), 36 (`$`), 37 (`%`), 38 (`&`), 39 (`'`), 40 (`(`), 41 (`)`), 42 (`*`), 43 (`+`), 44 (`,`), 45 (`-`), 46 (`.`), 47 (`/`), 58 (`:`), 59 (`;`), 60 (`<`), 61 (`=`), 62 (`>`), 63 (`?`), 64 (`@`), 91 (`[`), 92 (`\`), 93 (`]`), 94 (`^`), 95 (`_`), 96 (```), 123 (`{`), 124 (`|`), 125 (`}`), 126 (`~`), `[`127 - 255`]`  ||   http://host/path/to/page.ext/<font color="red">test%3Ca%22'%0A%60=%20+%20%3E;test%3Ca%22'%0A%60=%20+%20%3E</font><font color="green">?test%3Ca%22'%0A%60=%20+%20%3E;</font><font color="blue">#test<a"'%0A```= +%20>;</font>    ||
|| location.href ||   IE 8     ||  8       || 33 (`!`), 36 (`$`), 38 (`&`), 39 (`'`), 40 (`(`), 41 (`)`), 42 (`*`), 43 (`+`), 44 (`,`), 45 (`-`), 46 (`.`), 47 (`/`), 58 (`:`), 59 (`;`), 61 (`=`), 64 (`@`), 91 (`[`), 93 (`]`), 95 (`_`), 126 (`~`), `[`128 - 255`]`   ||  1, 2, 3, 4, 5, 6, 7, 8, 11, 12, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24, 25, 26, 27, 28, 29, 30, 31, 32 (` `), 33 (`!`), 34 (`"`), 36 (`$`), 38 (`&`), 39 (`'`), 40 (`(`), 41 (`)`), 42 (`*`), 43 (`+`), 44 (`,`), 45 (`-`), 46 (`.`), 47 (`/`), 58 (`:`), 59 (`;`), 60 (`<`), 61 (`=`), 62 (`>`), 63 (`?`), 64 (`@`), 91 (`[`), 92 (`\`), 93 (`]`), 94 (`^`), 95 (`_`), 96 (```), 123 (`{`), 124 (`|`), 125 (`}`), 126 (`~`), `[`127 - 255`]` || 1, 2, 3, 4, 5, 6, 7, 8, 11, 12, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24, 25, 26, 27, 28, 29, 30, 31, 32 (` `), 33 (`!`), 34 (`"`), 35 (`#`), 36 (`$`), 38 (`&`), 39 (`'`), 40 (`(`), 41 (`)`), 42 (`*`), 43 (`+`), 44 (`,`), 45 (`-`), 46 (`.`), 47 (`/`), 58 (`:`), 59 (`;`), 60 (`<`), 61 (`=`), 62 (`>`), 63 (`?`), 64 (`@`), 91 (`[`), 92 (`\`), 93 (`]`), 94 (`^`), 95 (`_`), 96 (```), 123 (`{`), 124 (`|`), 125 (`}`), 126 (`~`), `[`127 -  255`]` ||  http://host/path/to/page.ext/<font color="red">test%3Ca%22'%0A%60=%20+%20%3E;test%3Ca%22'%0A%60=%20+%20%3E</font><font color="green">?test<a"'%0A```=%20+%20><font color="blue">;#test<a"'%0A```=%20+%20>;</font>   ||
|| location.href ||     Firefox     ||  3.6.8       ||  33 (`!`), 36 (`$`), 37 (`%`), 38 (`&`), 40 (`(`), 41 (`)`), 42 (`*`), 43 (`+`), 44 (`,`), 45 (`-`), 46 (`.`), 47 (`/`), 58 (`:`), 59 (`;`), 61 (`=`), 64 (`@`), 91 (`[`), 92 (`\`), 93 (`]`), 94 (`^`), 95 (`_`), 123 (`{`), 124 (`|`), 125 (`}`), 126 (`~`) || 33 (`!`), 36 (`$`), 37 (`%`), 38 (`&`), 40 (`(`), 41 (`)`), 42 (`*`), 43 (`+`), 44 (`,`), 45 (`-`), 46 (`.`), 47 (`/`), 58 (`:`), 59 (`;`), 61 (`=`), 63 (`?`), 64 (`@`), 91 (`[`), 92 (`\`), 93 (`]`), 94 (`^`), 95 (`_`), 123 (`{`), 124 (`|`), 125 (`}`), 126 (`~`)  ||  33 (`!`), 35 (`#`), 36 (`$`), 37 (`%`), 38 (`&`), 40 (`(`), 41 (`)`), 42 (`*`), 43 (`+`), 44 (`,`), 45 (`-`), 46 (`.`), 47 (`/`), 58 (`:`), 59 (`;`), 61 (`=`), 63 (`?`), 64 (`@`), 91 (`[`), 92 (`\`), 93 (`]`), 94 (`^`), 95 (`_`), 123 (`{`), 124 (`|`), 125 (`}`), 126 (`~`) ||http://host/path/to/page.ext/<font color="red">test%3Ca%22%27%0A%60=%20+%20%3E;test%3Ca%22%27%0A%60=%20+%20%3E</font><font color="green">?test%3Ca%22%27%0A%60=%20+%20%3E;<font color="blue">#test%3Ca%22%27%0A%60=%20+%20%3E;</font>   ||
|| location.href ||     Chrome     ||   6.0.472.53 beta  || 33 (`!`), 36 (`$`), 37 (`%`), 38 (`&`), 39 (`'`), 40 (`(`), 41 (`)`), 42 (`*`), 43 (`+`), 44 (`,`), 45 (`-`), 46 (`.`), 47 (`/`), 58 (`:`), 59 (`;`), 61 (`=`), 64 (`@`), 91 (`[`), 93 (`]`), 95 (`_`), 126 (`~`) ||  33 (`!`), 36 (`$`), 37 (`%`), 38 (`&`), 39 (`'`), 40 (`(`), 41 (`)`), 42 (`*`), 43 (`+`), 44 (`,`), 45 (`-`), 46 (`.`), 47 (`/`), 58 (`:`), 59 (`;`), 61 (`=`), 63 (`?`), 64 (`@`), 91 (`[`), 92 (`\`), 93 (`]`), 94 (`^`), 95 (`_`), 96 (```), 123 (`{`), 124 (`|`), 125 (`}`), 126 (`~`) || 32 (` `), 33 (`!`), 34 (`"`), 35 (`#`), 36 (`$`), 37 (`%`), 38 (`&`), 39 (`'`), 40 (`(`), 41 (`)`), 42 (`*`), 43 (`+`), 44 (`,`), 45 (`-`), 46 (`.`), 47 (`/`), 58 (`:`), 59 (`;`), 60 (`<`), 61 (`=`), 62 (`>`), 63 (`?`), 64 (`@`), 91 (`[`), 92 (`\`), 93 (`]`), 94 (`^`), 95 (`_`), 96 (```), 123 (`{`), 124 (`|`), 125 (`}`), 126 (`~`), `[`127 -  255`]`  ||  http://host/path/to/page.ext/<font color="red">test%3Ca%22'%0A%60=%20+%20%3E;test%3Ca%22'%0A%60=%20+%20%3E</font><font color="green">?test%3Ca%22'%0A```=%20+%20%3E;<font color="blue">#test<a"'%0A```= +%20>;</font>   ||
|| location.href ||     Opera     ||  10.61       || 33 (`!`), 36 (`$`), 37 (`%`), 38 (`&`), 39 (`'`), 40 (`(`), 41 (`)`), 42 (`*`), 43 (`+`), 44 (`,`), 45 (`-`), 46 (`.`), 47 (`/`), 58 (`:`), 59 (`;`), 61 (`=`), 64 (`@`), 91 (`[`), 93 (`]`), 94 (`^`), 95 (`_`), 123 (`{`), 124 (`|`), 125 (`}`), 126 (`~`) || 33 (`!`), 36 (`$`), 37 (`%`), 38 (`&`), 39 (`'`), 40 (`(`), 41 (`)`), 42 (`*`), 43 (`+`), 44 (`,`), 45 (`-`), 46 (`.`), 47 (`/`), 58 (`:`), 59 (`;`), 61 (`=`), 63 (`?`), 64 (`@`), 91 (`[`), 93 (`]`), 94 (`^`), 95 (`_`), 123 (`{`), 124 (`|`), 125 (`}`), 126 (`~`) || 1, 2, 3, 4, 5, 6, 7, 8, 11, 12, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24, 25, 26, 27, 28, 29, 30, 31, 32 (` `), 33 (`!`), 34 (`"`), 35 (`#`), 36 (`$`), 37 (`%`), 38 (`&`), 39 (`'`), 40 (`(`), 41 (`)`), 42 (`*`), 43 (`+`), 44 (`,`), 45 (`-`), 46 (`.`), 47 (`/`), 58 (`:`), 59 (`;`), 60 (`<`), 61 (`=`), 62 (`>`), 63 (`?`), 64 (`@`), 91 (`[`), 92 (`\`), 93 (`]`), 94 (`^`), 95 (`_`), 96 (```), 123 (`{`), 124 (`|`), 125 (`}`), 126 (`~`), `[`127 - 255`]`  || http://host/path/to/page.ext/<font color="red">test%3Ca%22'%0A%60=%20+%20%3E;test%3Ca%22'%0A%60=%20+%20%3E</font><font color="green">?test%3Ca%22'%0A%60=%20+%20%3E;<font color="blue">#test<a"'%0A```= +%20>;</font>    ||
|| location.pathname ||   IE 8     ||  8       || 33 (`!`), 36 (`$`), 38 (`&`), 39 (`'`), 40 (`(`), 41 (`)`), 42 (`*`), 43 (`+`), 44 (`,`), 45 (`-`), 46 (`.`), 47 (`/`), 58 (`:`), 59 (`;`), 61 (`=`), 64 (`@`), 91 (`[`), 93 (`]`), 95 (`_`), 126 (`~`), `[`128 - 255`]`     || *No Search* || *No Hash* ||  /path/to/page.ext/<font color="red">test%3Ca%22'%0A%60=%20+%20%3E;test%3Ca%22'%0A%60=%20+%20%3E</font> ||
|| location.pathname ||    Firefox     ||  3.6.8        || 33 (`!`), 36 (`$`), 37 (`%`), 38 (`&`), 40 (`(`), 41 (`)`), 42 (`*`), 43 (`+`), 44 (`,`), 45 (`-`), 46 (`.`), 47 (`/`), 58 (`:`), 61 (`=`), 64 (`@`), 95 (`_`), 124 (`|`), 126 (`~`) || *No Search* || *No Hash* || /path/to/page.ext/<font color="red">test%3Ca%22%27%0A%60=%20+%20%3E</font> ||
|| location.pathname ||    Chrome     ||   6.0.472.53 beta     ||  33 (`!`), 36 (`$`), 37 (`%`), 38 (`&`), 39 (`'`), 40 (`(`), 41 (`)`), 42 (`*`), 43 (`+`), 44 (`,`), 45 (`-`), 46 (`.`), 47 (`/`), 58 (`:`), 59 (`;`), 61 (`=`), 64 (`@`), 91 (`[`), 93 (`]`), 95 (`_`), 126 (`~`) || *No Search* || *No Hash* || /path/to/page.ext/<font color="red">test%3Ca%22'%0A%60=%20+%20%3E;test%3Ca%22'%0A%60=%20+%20%3E</font> ||
|| location.pathname ||    Opera     ||  10.61        || 27, 32 (` `), 33 (`!`), 34 (`"`), 36 (`$`), 37 (`%`), 38 (`&`), 39 (`'`), 40 (`(`), 41 (`)`), 42 (`*`), 43 (`+`), 44 (`,`), 45 (`-`), 46 (`.`), 47 (`/`), 58 (`:`), 59 (`;`), 60 (`<`), 61 (`=`), 62 (`>`), 64 (`@`), 91 (`[`), 93 (`]`), 94 (`^`), 95 (`_`), 96 (```), 123 (`{`), 124 (`|`), 125 (`}`), 126 (`~`), `[`127-255`]`  || *No Search* || *No Hash* || /path/to/page.ext/<font color="red">test<a"'%0A```= + >;test<a"'%0A```= + ></font> ||
|| location.search ||   IE 8     ||  8       || *No pathName* || 1, 2, 3, 4, 5, 6, 7, 8, 11, 12, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24, 25, 26, 27, 28, 29, 30, 31, 32 (` `), 33 (`!`), 34 (`"`), 36 (`$`), 38 (`&`), 39 (`'`), 40 (`(`), 41 (`)`), 42 (`*`), 43 (`+`), 44 (`,`), 45 (`-`), 46 (`.`), 47 (`/`), 58 (`:`), 59 (`;`), 60 (`<`), 61 (`=`), 62 (`>`), 63 (`?`), 64 (`@`), 91 (`[`), 92 (`\`), 93 (`]`), 94 (`^`), 95 (`_`), 96 (```), 123 (`{`), 124 (`|`), 125 (`}`), 126 (`~`), `[`127-255`]`|| *No Hash* ||  <font color="green">?test<a"'%0A```=%20+%20>;</font>    ||
|| location.search ||    Firefox     ||  3.6.8        || *No pathName*  || 33 (`!`), 36 (`$`), 37 (`%`), 38 (`&`), 40 (`(`), 41 (`)`), 42 (`*`), 43 (`+`), 44 (`,`), 45 (`-`), 46 (`.`), 47 (`/`), 58 (`:`), 59 (`;`), 61 (`=`), 63 (`?`), 64 (`@`), 91 (`[`), 92 (`\`), 93 (`]`), 94 (`^`), 95 (`_`), 123 (`{`), 124 (`|`), 125 (`}`), 126 (`~`) || *No Hash* ||  <font color="green">?test%3Ca%22%27%0A%60=%20+%20%3E;</font>   ||
|| location.search ||      Chrome     ||   6.0.472.53 beta        || *No pathName*     ||  33 (`!`), 36 (`$`), 37 (`%`), 38 (`&`), 39 (`'`), 40 (`(`), 41 (`)`), 42 (`*`), 43 (`+`), 44 (`,`), 45 (`-`), 46 (`.`), 47 (`/`), 58 (`:`), 59 (`;`), 61 (`=`), 63 (`?`), 64 (`@`), 91 (`[`), 92 (`\`), 93 (`]`), 94 (`^`), 95 (`_`), 96 (```), 123 (`{`), 124 (`|`), 125 (`}`), 126 (`~`) || *No Hash* || <font color="green">?test%3Ca%22'%0A```=%20+%20%3E;</font>  ||
|| location.search ||    Opera     ||  10.61        ||  *No pathName* || 33 (`!`), 36 (`$`), 37 (`%`), 38 (`&`), 39 (`'`), 40 (`(`), 41 (`)`), 42 (`*`), 43 (`+`), 44 (`,`), 45 (`-`), 46 (`.`), 47 (`/`), 58 (`:`), 59 (`;`), 61 (`=`), 63 (`?`), 64 (`@`), 91 (`[`), 93 (`]`), 94 (`^`), 95 (`_`), 123 (`{`), 124 (`|`), 125 (`}`), 126 (`~`) || *No Hash* || <font color="green">?test%3Ca%22'%0A%60=%20+%20%3E;</font>    ||
|| location.hash ||   IE 8     ||  8       ||  *No pathName*   || *No Search* || 1, 2, 3, 4, 5, 6, 7, 8, 11, 12, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24, 25, 26, 27, 28, 29, 30, 31, 32 (` `), 33 (`!`), 34 (`"`), 35 (`#`), 36 (`$`), 38 (`&`), 39 (`'`), 40 (`(`), 41 (`)`), 42 (`*`), 43 (`+`), 44 (`,`), 45 (`-`), 46 (`.`), 47 (`/`), 58 (`:`), 59 (`;`), 60 (`<`), 61 (`=`), 62 (`>`), 64 (`@`), 91 (`[`), 92 (`\`), 93 (`]`), 94 (`^`), 95 (`_`), 96 (```), 123 (`{`), 124 (`|`), 125 (`}`), 126 (`~`), `[`127 - 255`]` ||<font color="blue">#test<a"'%0A```=%20+%20>;</font>   ||
|| location.hash ||     Firefox     ||  3.6.8       || *No pathName*  || *No Search* || 32 (` `), 33 (`!`), 34 (`"`), 35 (`#`), 36 (`$`), 37 (`%`), 38 (`&`), 39 (`'`), 40 (`(`), 41 (`)`), 42 (`*`), 43 (`+`), 44 (`,`), 45 (`-`), 46 (`.`), 47 (`/`), 58 (`:`), 59 (`;`), 60 (`<`), 61 (`=`), 62 (`>`), 64 (`@`), 91 (`[`), 92 (`\`), 93 (`]`), 94 (`^`), 95 (`_`), 96 (```), 123 (`{`), 124 (`|`), 125 (`}`), 126 (`~`), `[`128 - 255`]`  ||<font color="blue">#test<a"'%0A```= + >;</font>  ||
|| location.hash ||     Chrome     ||   6.0.472.53 beta    || *No pathName*   || *No Search* || 32 (` `), 33 (`!`), 34 (`"`), 35 (`#`), 36 (`$`), 37 (`%`), 38 (`&`), 39 (`'`), 40 (`(`), 41 (`)`), 42 (`*`), 43 (`+`), 44 (`,`), 45 (`-`), 46 (`.`), 47 (`/`), 58 (`:`), 59 (`;`), 60 (`<`), 61 (`=`), 62 (`>`), 64 (`@`), 91 (`[`), 92 (`\`), 93 (`]`), 94 (`^`), 95 (`_`), 96 (```), 123 (`{`), 124 (`|`), 125 (`}`), 126 (`~`), `[`127 - 255 `]`||<font color="blue">#test<a"'%0A```= +%20>;</font>  ||
|| location.hash ||     Opera     ||  10.61       || *No pathName*  || *No Search* || 1, 2, 3, 4, 5, 6, 7, 8, 11, 12, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24, 25, 26, 27, 28, 29, 30, 31, 32 (` `), 33 (`!`), 34 (`"`), 35 (`#`), 36 (`$`), 37 (`%`), 38 (`&`), 39 (`'`), 40 (`(`), 41 (`)`), 42 (`*`), 43 (`+`), 44 (`,`), 45 (`-`), 46 (`.`), 47 (`/`), 58 (`:`), 59 (`;`), 60 (`<`), 61 (`=`), 62 (`>`), 64 (`@`), 91 (`[`), 92 (`\`), 93 (`]`), 94 (`^`), 95 (`_`), 96 (```), 123 (`{`), 124 (`|`), 125 (`}`), 126 (`~`), `[`127 - 255`]` ||  <font color="blue">#test<a"'%0A```= +%20>;</font>   ||

(To Be Finished with Safari tests) 
 
=== The Cookies Sources ===

Characters in Cookie values are invariant to the way they have been given.
Which means that if a !JavaScript application sets:
<code language="javascript">
document.cookie="PREF=a\x01b; expires=Sun, 09-Sep-2012 06:38:09 GMT; path=/; domain=.host.tld"
</code>

the resulting cookie will be:
{{{
"PREF=ab;"
//for browsers that don't show the whole string, "a\x01b" 
}}}

For what concerns setting cookie precedence from two different hostnames sharing the same subdomain Kuza55 gives a very good compound [#References [4]] about browsers behavior.

In particular quoted:
{{{
 Resolving Conflicts

 But what if two cookies of the same name should be sent to a given page, e.g. 
 if there is a cookie called "user" set for mail.google.com and .google.com with 
 different values, how does the browser decide which one to send?
 
 RFC 2109 states that the cookie with the more specific path attribute must be 
 sent first, however it does not define how to deal with two cookies which have 
 the same path (e.g. /) but different domains. If such a conflict occurs then 
 most (all?) browsers simply send the older cookie first.
 
 This means that if we want to overwrite a cookie on mail.google.com from the
 subdomain news.google.com, and the cookie already exists, then we cannot over-write
 a cookie with the path value of / (or whatever the path value of the existing
 cookie is), but we can override it for every other path (up to the maximum number
 of cookies allowed per host; 50 in IE/Firefox 30 in Opera), i.e. if we pick 50
 (or 30 if we want to target opera) paths on mail.google.com which encompass the
 directories and pages we want to overwrite the cookie for, we can simply set
 50 /30 separate cookies which are all more specific than the existing cookie.
}}}


Also Kuza55 talks about paths:
{{{
Technically the spec say that a.b.c.d cannot set a cookie for a.b.c.d or b.c.d 
only, none of the browsers enforce this since it breaks sites. 
Also, sites should not be able to set a cookie with a path attribute which would
 not apply to the current page, but since path 
boundaries are non-existant in browsers, no-one enforces this restriction either.
}}}

From a Javascript cookie string perspective, multiple cookies with same name are
returned.

Which means that given two hosts with same domain:
{{{
Time t - From: vi.ct.im/path/to/page/
document.cookie="SESSION=TRUESESSION; path=/";

Time t+1 - From: v2.ct.im/another/path/to/a/page/
document.cookie="SESSION=FAKESESSION; path=/path/to/page; domain=.ct.im"

Time t+2 - From: vi.ct.im/path/to/page/
document.cookie
returns 
"SESSION=FAKESESSION; SESSION=TRUESESSION;"
}}}

Usually getCookie functions from javaScript get the first occurrence of the cookie name, so, in this very case, the FAKESESSION value will be returned.
{{{
getCookie = function (name) {
  var search = name + '=';
  var returnValue = '';

  if (document.cookie.length > 0) {
    offset = document.cookie.indexOf(search);
    if (offset != -1) {
      offset += search.length;
      var end = document.cookie.indexOf(';', offset);
      if (end == -1) {
        end = document.cookie.length;
      }
      returnValue = decodeURIComponent(document.cookie.substring(offset, end).replace(/\+/g, '%20'));
    }
  }

  return returnValue;
};
}}}
Of course if the function returns the last occurrence of the name in cookie string, the attacker will force a very generic cookie from vi2.ct.im:
{{{
  From: v2.ct.im/another/path/to/a/page/
document.cookie="SESSION=FAKESESSION; path=/; domain=.ct.im"
}}}

This can be considered a case of Parameter Pollution in Cookies [#References [5]].

Depending on how the !JavaScript application will later use specific cookie values, this manipulation can be used to inject attacker controlled inputs and use them not only for Session Fixation but also to control !JavaScript flow or to perform classic DOMXss.



=== The Referrer Source ===
The following table shows how direct call of

 * document.referrer

are natively treated:

|| *Source* || *browser* || *version* ||  *pathInfo* || *Search* || *Hash* || *output sample*||
|| document.referrer ||     IE 8     ||  8        || 33 (`!`), 38 (`&`), 39 (`'`), 40 (`(`), 41 (`)`), 42 (`*`), 43 (`+`), 44 (`,`), 45 (`-`), 46 (`.`), 47 (`/`), 58 (`:`), 59 (`;`), 61 (`=`), 64 (`@`), 91 (`[`), 93 (`]`), 95 (`_`), 126 (`~`), `[`128 - 255`]` || 1, 2, 3, 4, 5, 6, 7, 8, 11, 12, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24, 25, 26, 27, 28, 29, 30, 31, 32 (` `), 33 (`!`), 34 (`"`), 38 (`&`), 39 (`'`), 40 (`(`), 41 (`)`), 42 (`*`), 43 (`+`), 44 (`,`), 45 (`-`), 46 (`.`), 47 (`/`), 58 (`:`), 59 (`;`), 60 (`<`), 61 (`=`), 62 (`>`), 63 (`?`), 64 (`@`), 91 (`[`), 92 (`\`), 93 (`]`), 94 (`^`), 95 (`_`), 96 (```), 123 (`{`), 124 (`|`), 125 (`}`), 126 (`~`), `[`127 - 255`]` || none || http://host/path/to/page.ext/<font color="red">test%3Ca%22%27%0A%60=%20+%20%3E;test%3Ca%22%27%0A%60=%20+%20%3E</font><font color="green">?test%3Ca%22%27%0A%60=%20+%20%3E;</font>    ||
|| document.referrer ||     Firefox    ||  3.6.8      || 33 (`!`), 37 (`%`), 38 (`&`), 40 (`(`), 41 (`)`), 42 (`*`), 43 (`+`), 44 (`,`), 45 (`-`), 46 (`.`), 47 (`/`), 58 (`:`), 59 (`;`), 61 (`=`), 64 (`@`), 91 (`[`), 92 (`\`), 93 (`]`), 94 (`^`), 95 (`_`), 123 (`{`), 124 (`|`), 125 (`}`), 126 (`~`) || 33 (`!`), 37 (`%`), 38 (`&`), 40 (`(`), 41 (`)`), 42 (`*`), 43 (`+`), 44 (`,`), 45 (`-`), 46 (`.`), 47 (`/`), 58 (`:`), 59 (`;`), 61 (`=`), 63 (`?`), 64 (`@`), 91 (`[`), 92 (`\`), 93 (`]`), 94 (`^`), 95 (`_`), 123 (`{`), 124 (`|`), 125 (`}`), 126 (`~`) || None  ||   http://host/path/to/page.ext/<font color="red">test%3Ca%22'%0A%60=%20+%20%3E;test%3Ca%22'%0A%60=%20+%20%3E</font><font color="green">?test<a"'%0A```=%20+%20>;</font>    ||
|| document.referrer ||       Chrome     ||   6.0.472.53 beta        || 33 (`!`), 37 (`%`), 38 (`&`), 39 (`'`), 40 (`(`), 41 (`)`), 42 (`*`), 43 (`+`), 44 (`,`), 45 (`-`), 46 (`.`), 47 (`/`), 58 (`:`), 59 (`;`), 61 (`=`), 64 (`@`), 91 (`[`), 93 (`]`), 95 (`_`), 126 (`~`)  ||  33 (`!`), 37 (`%`), 38 (`&`), 39 (`'`), 40 (`(`), 41 (`)`), 42 (`*`), 43 (`+`), 44 (`,`), 45 (`-`), 46 (`.`), 47 (`/`), 58 (`:`), 59 (`;`), 61 (`=`), 63 (`?`), 64 (`@`), 91 (`[`), 92 (`\`), 93 (`]`), 94 (`^`), 95 (`_`), 96 (```), 123 (`{`), 124 (`|`), 125 (`}`), 126 (`~`) || None || http://host/path/to/page.ext/<font color="red">test%3Ca%22'%0A%60=%20+%20%3E;test%3Ca%22'%0A%60=%20+%20%3E</font><font color="green">?test%3Ca%22'%0A`=%20+%20%3E;</font>    ||
|| document.referrer ||       Opera     ||  10.61    || 33 (`!`), 37 (`%`), 38 (`&`), 39 (`'`), 40 (`(`), 41 (`)`), 42 (`*`), 43 (`+`), 44 (`,`), 45 (`-`), 46 (`.`), 47 (`/`), 58 (`:`), 59 (`;`), 61 (`=`), 64 (`@`), 91 (`[`), 93 (`]`), 94 (`^`), 95 (`_`), 96 (```), 123 (`{`), 124 (`|`), 125 (`}`), 126 (`~`), `[`127 - 255`]`  || 33 (`!`), 37 (`%`), 38 (`&`), 39 (`'`), 40 (`(`), 41 (`)`), 42 (`*`), 43 (`+`), 44 (`,`), 45 (`-`), 46 (`.`), 47 (`/`), 58 (`:`), 59 (`;`), 61 (`=`), 63 (`?`), 64 (`@`), 91 (`[`), 93 (`]`), 94 (`^`), 95 (`_`), 123 (`{`), 124 (`|`), 125 (`}`), 126 (`~`) || None    ||   http://host/path/to/page.ext/<font color="red">test%3Ca%22'%0A```=%20+%20%3E;test%3Ca%22'%0A`=%20+%20%3E</font><font color="green">?test%3Ca%22'%0A%60=%20+%20%3E;</font>    ||

(To Be Finished with Safari tests) 

=== The Window Name Source === 

Characters in window.name value are invariant to the way they have been given.
Which means that if a !JavaScript application sets:

{{{
window.name='a\x01b'
}}}

no encoding is applied.

Window.name attribute is always a cast to the string representation of the object it is assigned to.

The window.name attribute is a persistent value during the existence of the page to which is assigned.

An attacker can set new windows names and frames with no restriction, and they will persist during navigation on any domain.

=== Indirect Sources ===

(TBA)

==== Storage Object ====

HTML 5 Storage objects [#References [6]][#References  [7]][#References [8] ] can be considered an indirect source, since they can be used to store values from direct sources and use them later insecurely.

Indirect source objects are:

 * localStorage 
 * sessionStorage
 * Database (Safari Only)

==== Server Response Sources ====

Previously server side stored data could be used by an attacker to send untrusted input
to Javascript.

(TBF)

=== Other Objects Sources ===

(TBA)

 * opener (IE <= 7 Only)
 * parent/top/frames`[`i`]`.obj
 * event.data of onmessage event for postMessage method

==== Opener ====

In 2008 in [#References [[3]]] it was presented a study about Browser Based DOM Xss, describing how browsers behave when objects belonging to different windows and domains are overwritten or deleted from evil pages.

It was found that IE <= 7 allows cross windows/cross domain opener redefinition, causing the re-instantiation of the object in the other window thus breaking the SOP in access control.

{{{
// From attacker.tld
window.aFrame.location="http://victim/PageUsingOpenerObject.html"
window.aFrame.opener={someAttr:"someValue", someAttr2: function(){return someReturnValue}}
}}}

So if a page from victim host uses:
{{{
<script>
document.writeln("<p>" + window.opener.Message + "</p>");
</script>
}}}

An attacker can use from {{{<iframe name=aFrame></iframe>}}}
{{{
// From attacker.tld
window.aFrame.location="http://victim/PageUsingOpenerObject.html"
window.aFrame.opener={Message:"<sc"+"ript>alert(document.domain)</scr"+"ipt>"}
}}}

The code above works perfectly on IE7 and the fake Message is taken by victim host, without any error message.

Opener object can, hence, be considered as a source of untrusted input in the unfortunate case the victim uses IE 7.

N.B. IE 8 fixes this issue.

== Sinks ==
(TBA)
=== Execution Sinks ===
(TBA)
=== Set Object Sinks ===
(TBA)
=== HTMLElement Sinks ===
(TBA)
=== Style Sinks ===
(TBA)
=== XMLHttpRequest Sink ===
(TBA)
=== Set Cookie Sink ===
(TBA)
=== Set Location Sink ===
(TBA)
=== Control Flow Sink ===
(TBA)
=== Use of Equality And Strict Equality ===
(TBA)
=== Math.random Sink ===
(TBA)
=== JSON Sink ===
(TBA)
=== XML Sink ===
(TBA)

= Glossary =

*Source:*
an input that could be controlled by an external (untrusted) source.

*Sink:*
a sink is a potentially dangerous method that could lead to a vulnerability.
In this case a DOM Based Xss.

= References =
`[`1`]` [http://www.webappsec.org/projects/articles/071105.shtml "DOM Based Cross Site Scripting or XSS of the Third Kind"], A. Klein, 2005.

`[`2`]` [http://blog.watchfire.com/wfblog/2008/06/javascript-code.html "JavaScript Code Flow Manipulation, and a real world example advisory - Adobe Flex 3 Dom-Based XSS"], O. Segal & A. Sharabani, A. Yogev, June 2008.

`[`3`]` [http://www.ruxcon.org.au/files/2008/Attacking_Rich_Internet_Applications.pdf Attacking_Rich_Internet_Applications], S. Di Paola & A. Kuza, 2008.

`[`4`]` [http://kuza55.blogspot.com/2008/02/understanding-cookie-security.html Understanding Cookie Security] , A. Kuza, February 22, 2008.

`[`5`]` [http://www.owasp.org/images/b/ba/AppsecEU09_CarettoniDiPaola_v0.8.pdf Http Parameter Pollution] , L. Carettoni S. Di Paola, 2009. 

`[`6`]` [http://dev.w3.org/html5/webdatabase/ W3C ClientSide Database]

`[`7`]` [http://dev.w3.org/html5/webstorage W3C Web Storage]

`[`8`]` [http://msdn.microsoft.com/en-us/library/cc197062%28VS.85%29.aspx Microsoft's Introduction to DOM Storage]
