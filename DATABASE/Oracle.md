ip地址排序
```
order by regexp_substr(ip,'[^.]+',1,1)+0,regexp_substr(ip,'[^.]+',1,2)+0,
         regexp_substr(ip,'[^.]+',1,3)+0,regexp_substr(ip,'[^.]+',1,4)+0
```
