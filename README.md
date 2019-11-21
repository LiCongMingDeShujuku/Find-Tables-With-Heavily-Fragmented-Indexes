![CLEVER DATA GIT REPO](https://raw.githubusercontent.com/LiCongMingDeShujuku/git-resources/master/0-clever-data-github.png "李聪明的数据库")

# 查找具有重度碎片索引的表格
#### Find Tables With Heavily Fragmented Indexes
**TIME STAMP**

![#](images/##############?raw=true "#")

## Contents

- [中文](#中文)
- [English](#English)
- [SQL Logic](#Logic)
- [Build Info](#Build-Info)
- [Author](#Author)
- [License](#License) 


## 中文
下面是查找重度碎片索引的表格的快速方法。用来查找超过70％碎片的表格。用其进行定期维护工作中是个不错的主意，你只需重新制作那些超过70％到80％碎片的作业。通过重组，你也可以查询任何低于这个百分比的表格。


## English
Here’s quick way to find Tables that have heavily fragmented indexes. This is designed to find tables that are above 70% fragmentation. It’s a good idea to incorporate this into a regularly scheduled maintenance job, and just REBUILD those that are above 70% to 80% fragmentation. Anything below this point can simply be REORGANIZED.

---
## Logic
```SQL
select
'database_name' = db_name(sddips.database_id)
,   'table_name' = object_name(sddips.object_id)
,   'object type' = ist.table_type
,   'fragmentation' = left(sddips.avg_fragmentation_in_percent, 4) from
sys.dm_db_index_physical_stats (db_id(), null, null, null, null) sddips
join information_schema.TABLES ist on object_name(sddips.object_id) = ist.table_name where
ist.table_type = 'base table' and sddips.avg_fragmentation_in_percent &gt; 70 order by
sddips.avg_fragmentation_in_percent desc;


```



[![WorksEveryTime](https://forthebadge.com/images/badges/60-percent-of-the-time-works-every-time.svg)](https://shitday.de/)

## Build-Info

| Build Quality | Build History |
|--|--|
|<table><tr><td>[![Build-Status](https://ci.appveyor.com/api/projects/status/pjxh5g91jpbh7t84?svg?style=flat-square)](#)</td></tr><tr><td>[![Coverage](https://coveralls.io/repos/github/tygerbytes/ResourceFitness/badge.svg?style=flat-square)](#)</td></tr><tr><td>[![Nuget](https://img.shields.io/nuget/v/TW.Resfit.Core.svg?style=flat-square)](#)</td></tr></table>|<table><tr><td>[![Build history](https://buildstats.info/appveyor/chart/tygerbytes/resourcefitness)](#)</td></tr></table>|

## Author

- **李聪明的数据库 Lee's Clever Data**
- **Mike的数据库宝典 Mikes Database Collection**
- **李聪明的数据库** "Lee Songming"

[![Gist](https://img.shields.io/badge/Gist-李聪明的数据库-<COLOR>.svg)](https://gist.github.com/congmingshuju)
[![Twitter](https://img.shields.io/badge/Twitter-mike的数据库宝典-<COLOR>.svg)](https://twitter.com/mikesdatawork?lang=en)
[![Wordpress](https://img.shields.io/badge/Wordpress-mike的数据库宝典-<COLOR>.svg)](https://mikesdatawork.wordpress.com/)

---
## License
[![LicenseCCSA](https://img.shields.io/badge/License-CreativeCommonsSA-<COLOR>.svg)](https://creativecommons.org/share-your-work/licensing-types-examples/)

![Lee Songming](https://raw.githubusercontent.com/LiCongMingDeShujuku/git-resources/master/1-clever-data-github.png "李聪明的数据库")

