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
cat access.log | awk -F'[][]' '{split($2,t,":"); m=t[1]":"t[2]; c[m]++} END{for(m in c) print m, c[m]}' access.log | sort -nr -k 5 | head -5
Jan 09 2026, 22:04 2
Jan 13 2026, 08:25 1
Jan 13 2026, 07:40 1
Jan 13 2026, 07:22 1
Jan 13 2026, 06:38 1
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
