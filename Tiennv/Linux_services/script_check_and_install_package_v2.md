#!/bin/bash
a=("httpd" "mtr")
for i in "${a[@]}"
do
if rpm -q $i > /dev/null
then
       echo "$i da duoc cai dat"
else
       echo "$i dang duoc cai dat"
       yum install -y $i > /dev/null
       check=`echo $?`
       if [ $check == 0 ]
       then
               echo "$i da duoc cai dat thanh cong"
       else
               echo "cai dat $i that bai"
       fi
fi
done
