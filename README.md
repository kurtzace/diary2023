# diary2023


## courses

### How to export and report your learning progress

[Mid 2023 output](https://github.com/kurtzace/diary2023/blob/main/trainings2023.csv)

#### Udemy
- Open Udemy
- Login
- Open developer tools (ctrl shift I)
- Open my learning.
- See network tab and you will see a call similar to 
```
https://www.udemy.com/api-2.0/users/me/subscribed-courses/?ordering=-last_accessed&fields[course]=archive_time,buyable_object_type,completion_ratio,enrollment_time,favorite_time,features,image_240x135,image_480x270,is_practice_test_course,is_private,is_published,last_accessed_time,num_collections,published_title,title,tracking_id,url,visible_instructors&fields[user]=@min,job_title&page=1&page_size=12&is_archived=false
```
Save response as json object

run this in console.

```
json.results.forEach(x=>console.log(`${x.title};udemy;${x.completion_ratio};${x.last_accessed_time};${x.visible_instructors[0].title}`))
```

Paste in new notepad

save as .csv

Optionally add 

sep=;

as line 1


### Pluralsight
- Open Pluralsight
- Login
- Open developer tools (ctrl shift I)
- Open profile
- In network tab save responses of 

```
call
/profile/data/completedcourses/karanbhandari
and 
/profile/data/currentlylearning/karanbhandari
```
copy responses and run
```
json.forEach(x=>console.log(`${x.title};pluralsight;${x.percentComplete};${x.lastViewedTimestamp?x.lastViewedTimestamp:x.timeCompleted};${x.authors[0]?.displayName}`))

```


### Youtube

https://takeout.google.com/settings/takeout/downloads

Create new export

Deselect all

Unselect all types and only select Youtube history

![image](https://user-images.githubusercontent.com/2136211/236657252-935634af-f391-4925-9590-5a377a1ac7b8.png)


Search for youtube>select

select JSON

![image](https://user-images.githubusercontent.com/2136211/236657276-4147ac0b-80c7-434e-aa40-e062dbced6da.png)
 
 
 Click on Next/proceed
 
 Visit takeout after some time
 
 Download
 
 
 assign json as entire youtube json 
 
 then
 ```
 
let blacklist = ["hit","cardio","morning","property","hindi","deepak","melvin","song","choreo","danc",
"monkey","jcb","workout","dumb","icc","ipl","trailer","animal","fnp","car","phone","sams","onep","recipe",
"bjp","news","rhym","song","baby","melon","stretch","kettle"];

console.log(json.filter(x=>x.time.indexOf("2023")>-1).filter(x=>!blacklist.some(s => x.title.toLowerCase().includes(s))).length);


json.filter(x=>x.time.indexOf("2023")>-1).filter(x=>!blacklist.some(s => x.title.toLowerCase().includes(s))).forEach(x=>console.log(`${x.title};youtube;NA;${x.time};${x.titleUrl}`));

```
