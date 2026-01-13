# Task 2

##top 5 IP addresses requests come from:

```cat access.log | awk '{print $1}' | sort | uniq -c | sort -nr | head -5

      1 97.139.58.147
      1 93.184.208.27
      1 9.8.109.198
      1 9.193.86.5
      1 9.168.148.225
```

##number of requests with '50X' and '200' HTTP response codes:

```
cat access.log | awk '{print $11}' | sort | uniq -c | sort -nr
     53 200
     26 404
     24 403
     21 500
     21 304
     20 302
     18 400
     17 301

[Or viewing complete stings separately:]
5XX response:
cat access.log | awk '$11 ~ /^5[0-9]{2}+$/ {print}' 

200 response:
cat access.log | awk '$11 ~ /^200$/ {print}'
```

##number of requests per minute:

```
cat access.log | cut -d ' ' -f 4-7 | awk -F'[:,]' '{key=$1":"$2; count[key]++} END {for (i in count) print i " = " count[i] " requests"}' | sort
[Jan 06 2026: 10 = 3 requests
[Jan 06 2026: 11 = 3 requests
[Jan 06 2026: 15 = 1 requests
[Jan 06 2026: 16 = 1 requests
[Jan 06 2026: 17 = 2 requests
[Jan 06 2026: 18 = 3 requests
[Jan 06 2026: 20 = 4 requests
[Jan 06 2026: 22 = 2 requests
[Jan 06 2026: 23 = 2 requests
[Jan 07 2026: 00 = 3 requests
[Jan 07 2026: 01 = 1 requests
[Jan 07 2026: 02 = 1 requests
[Jan 07 2026: 03 = 2 requests
[Jan 07 2026: 04 = 1 requests
[Jan 07 2026: 06 = 1 requests
[Jan 07 2026: 07 = 3 requests
[Jan 07 2026: 08 = 1 requests
[Jan 07 2026: 10 = 1 requests
[Jan 07 2026: 11 = 1 requests
[Jan 07 2026: 12 = 2 requests
[Jan 07 2026: 14 = 2 requests
[Jan 07 2026: 16 = 1 requests
[Jan 07 2026: 17 = 2 requests
[Jan 07 2026: 21 = 1 requests
[Jan 07 2026: 23 = 1 requests
[Jan 08 2026: 00 = 1 requests
[Jan 08 2026: 01 = 2 requests
[Jan 08 2026: 02 = 1 requests
[Jan 08 2026: 03 = 2 requests
[Jan 08 2026: 05 = 1 requests
[Jan 08 2026: 06 = 2 requests
[Jan 08 2026: 07 = 3 requests
[Jan 08 2026: 08 = 1 requests
[Jan 08 2026: 09 = 3 requests
[Jan 08 2026: 11 = 1 requests
[Jan 08 2026: 13 = 1 requests
[Jan 08 2026: 16 = 1 requests
[Jan 08 2026: 18 = 2 requests
[Jan 08 2026: 20 = 1 requests
[Jan 08 2026: 21 = 2 requests
[Jan 08 2026: 23 = 1 requests
[Jan 09 2026: 03 = 2 requests
[Jan 09 2026: 05 = 3 requests
[Jan 09 2026: 06 = 2 requests
[Jan 09 2026: 08 = 1 requests
[Jan 09 2026: 09 = 1 requests
[Jan 09 2026: 10 = 3 requests
[Jan 09 2026: 11 = 1 requests
[Jan 09 2026: 12 = 1 requests
[Jan 09 2026: 13 = 1 requests
[Jan 09 2026: 14 = 3 requests
[Jan 09 2026: 15 = 3 requests
[Jan 09 2026: 16 = 1 requests
[Jan 09 2026: 17 = 1 requests
[Jan 09 2026: 18 = 2 requests
[Jan 09 2026: 19 = 3 requests
[Jan 09 2026: 20 = 1 requests
[Jan 09 2026: 21 = 1 requests
[Jan 09 2026: 22 = 3 requests
[Jan 09 2026: 23 = 2 requests
[Jan 10 2026: 00 = 1 requests
[Jan 10 2026: 01 = 2 requests
[Jan 10 2026: 02 = 3 requests
[Jan 10 2026: 03 = 3 requests
[Jan 10 2026: 04 = 4 requests
[Jan 10 2026: 05 = 1 requests
[Jan 10 2026: 06 = 1 requests
[Jan 10 2026: 07 = 1 requests
[Jan 10 2026: 08 = 1 requests
[Jan 10 2026: 10 = 4 requests
[Jan 10 2026: 11 = 1 requests
[Jan 10 2026: 14 = 2 requests
[Jan 10 2026: 16 = 1 requests
[Jan 10 2026: 18 = 1 requests
[Jan 10 2026: 19 = 2 requests
[Jan 10 2026: 21 = 4 requests
[Jan 10 2026: 23 = 2 requests
[Jan 11 2026: 00 = 2 requests
[Jan 11 2026: 01 = 2 requests
[Jan 11 2026: 04 = 1 requests
[Jan 11 2026: 05 = 2 requests
[Jan 11 2026: 07 = 1 requests
[Jan 11 2026: 08 = 1 requests
[Jan 11 2026: 10 = 2 requests
[Jan 11 2026: 11 = 3 requests
[Jan 11 2026: 12 = 2 requests
[Jan 11 2026: 13 = 1 requests
[Jan 11 2026: 14 = 4 requests
[Jan 11 2026: 17 = 1 requests
[Jan 11 2026: 18 = 1 requests
[Jan 11 2026: 21 = 2 requests
[Jan 11 2026: 23 = 1 requests
[Jan 12 2026: 00 = 1 requests
[Jan 12 2026: 02 = 1 requests
[Jan 12 2026: 03 = 1 requests
[Jan 12 2026: 04 = 2 requests
[Jan 12 2026: 06 = 2 requests
[Jan 12 2026: 07 = 1 requests
[Jan 12 2026: 08 = 1 requests
[Jan 12 2026: 09 = 1 requests
[Jan 12 2026: 10 = 1 requests
[Jan 12 2026: 12 = 1 requests
[Jan 12 2026: 13 = 1 requests
[Jan 12 2026: 16 = 1 requests
[Jan 12 2026: 17 = 1 requests
[Jan 12 2026: 19 = 2 requests
[Jan 12 2026: 22 = 2 requests
[Jan 12 2026: 23 = 2 requests
[Jan 13 2026: 00 = 1 requests
[Jan 13 2026: 01 = 1 requests
[Jan 13 2026: 02 = 1 requests
[Jan 13 2026: 03 = 1 requests
[Jan 13 2026: 04 = 3 requests
[Jan 13 2026: 05 = 2 requests
[Jan 13 2026: 06 = 2 requests
[Jan 13 2026: 07 = 2 requests
[Jan 13 2026: 08 = 1 requests
```

##which method is the most frequent one?:

```
cat access.log | awk -F '[" ]' '{print $9}' | sort | uniq -c | sort -nr 
     91 GET
     42 DELETE
     37 PUT
     30 POST
```
##any other improvements you can recommend to server admin based on the access log?:

```From the server-side perspective, plenty requests from crawlers may create unwanted load so we may suggest blocking them. Otherwise, more details are needed to provide suggestions.```
