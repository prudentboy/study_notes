## Hadoop学习 ##

 - first case  
脚本文件包含：start.sh；mapper.sh；reducer.sh
```
### start.sh ###
#!/bin/bash
haddop="/opt/hadoop-client/hadoop_maserati/bin/hadoop"
date_str=$(date -d"3 hour ago" "+%Y%m%d%H")
echo "-------------- ${day}   start----------------"
if [ ! -z $1 ];then
   date_str=$1
fi

day=$(echo ${date_str:0:8})
month=$(echo ${date_str:0:6})
hour=$(echo ${date_str:8:10})
echo $date_str, $day,$month,$hour
out="*****/$date_str"
log="****************"
file_name_src="result_${day}_${hour}"
local_out=result_${day}_$hour
#if [ ! -f $file_name_src ];then
 $adtf_haddop fs -rmr $out
 $adtf_haddop streaming -input $log \
                   -output $out \
                   -mapper "sh mapper.sh" \
                   -reducer "sh reducer.sh"\
                   -file mapper.sh reducer.sh \
                   -jobconf mapred.job.name='********' 
                   #-numReduceTasks 50
# $adtf_haddop fs -getmerge $local_out 
#fi

### mapper.sh ###
awk -F'\t' '{
    url_list=$NF;
    if(NF>1037) {
        url_list=$1037
    }
    filename=ENVIRON["map_input_file"];
    n=split(filename, name, ".");
    ip=name[n-3]"."name[n-2]"."name[n-1]"."name[n];
    n=split(url_list, ar, ";");
    for (i=1;i<=n; ++i) {
        url=ar[i];
        if (url ~/bill_un/) {
            continue;
        }
        if (url~/service.com/) {
            next;
        }
        if (url)
            printf("%s\3%s\t%s\n", ip, url, 1);
    }
}' $*

### reducer.sh ###
awk -F'\t' '{
    newkey=$1
    if (key==newkey) {
        count++;
    }
    else {
        if (key) {
            printf("%s\t%s\n", key, count);
        }
        key=newkey;
        count=1;
    }
}' $*
```
 - 查看输出  
```
##hadoopdir为hadoop执行bin文件路径
##cat可替换为其他shell命令，如ls等
hadoopdir fs -cat outputfile
##由于hadoopdir往往比较长，可结合export使用，如下例：
export adtf_hadoop="/opt/hadoop-client/hadoop_maserati/bin/hadoop"
$adtf_hadoop fs -ls *******
```
