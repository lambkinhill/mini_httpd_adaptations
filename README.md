# mini_httpd_adaptations
* some adaptations for mini_httpd-1.30 
* original author copyright: https://github.com/lambkinhill/mini_httpd_adaptations/blob/main/mini_httpd_copyright.txt

## Compiler error on Ubuntu 20.04 64bit
```
mini_httpd.c:102:19: error: conflicting types for ‘int64_t’
  102 | typedef long long int64_t;
      |                   ^~~~~~~
```

place lines 101-103 of original source mini_httpd.c inside a comment:

```
/* #ifndef HAVE_INT64T
typedef long long int64_t;
#endif */
```


## Allow CORS, modify header

add the 3 following lines to original source mini_httpd.c starting line 2601, adapt to your needs if you do not
want to allow all sources:
 
```
/* add 2 lines below to Allow CORS: Access-Control-Allow-Origin for all sources */
(void) snprintf( buf, sizeof(buf), "Access-Control-Allow-Origin: * \015\012");
add_to_response( buf );
```

## disable directory listing

add one following line to original source mini_httpd.c at line 1660:

```
send_error( 403, "Forbidden", "", "Directory is protected." );
```
