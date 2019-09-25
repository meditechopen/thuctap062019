#!/bin/bash
echo "Nhap so luong package"
read -e num
a=()
for ((i=1;i<=num;i++))
do
echo "Nhap package $i"
read -e a[i]
done
sleep 2;
echo "Bat dau check"
sleep 5;

for i in "${a[@]}"
do
if rpm -q $i > /dev/null
then
       echo "$i da duoc cai dat"
        sleep 2;
else
       echo "$i chua duoc cai dat"
        sleep 2;
        echo "Installing $i ..."
        sleep 5;
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