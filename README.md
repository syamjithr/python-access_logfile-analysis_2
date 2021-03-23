# python-access_logfile-analysis_2
# Log file Analysis using Python_2
You can use simple python codes to organize and analyze your log files like access_log. The bleow code will return a chat with date, Max num of hits from an individual ip and total number of hits. For ploting the chat we used  matplotlib.pyplot module.
```
counter = {}  

log = open('access.log')

for logLine in log:

  logParts = logLine.split()

  logIp = logParts[0]
  logDate = logParts[3].lstrip('[')[0:11]

  if logDate not in counter:
        
    counter[logDate] = {}
    
    if logIp not in counter[logDate]:
        
      counter[logDate].update({logIp:1})
        
  else:
    
    if logIp not in counter[logDate]:
      
      counter[logDate].update({logIp:1})
        
    else:
        
      counter[logDate][logIp] = counter[logDate][logIp] + 1
    
    

log.close()
```
```
import matplotlib.pyplot as plt
Date = []
Hits = []
for date in counter:
  hitPerDay = counter[date]
  totalhit = 0
  for ip in hitPerDay:
    hitPerip = hitPerDay[ip]
    firsthit = hitPerip
    totalhit = totalhit + firsthit
  Date.append(date)
  Hits.append(totalhit)
    
    
ip_List = []
MaxHit = []
for item in counter:
  
  keys_list = list(counter[item].keys())
  values_list = list(counter[item].values())
  Max_hit = max(values_list)
  position = values_list.index(Max_hit)
  ip = keys_list[position]
  ip_List.append(ip)
  MaxHit.append(Max_hit)
    
plt.figure(figsize=(10, 10))
plt.title('HitPerDay')
plt.ylabel('Days')
plt.xlabel('Hits')
plt.barh(Date,Hits,label="Total Num of Hits")
plt.barh(Date,MaxHit,label="Max num of hits from an individual ip")
plt.legend()
```
#### output
