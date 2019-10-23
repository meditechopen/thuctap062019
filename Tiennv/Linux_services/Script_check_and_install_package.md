#!/bin/bash
#Luu y: phai co internet moi cai dat duoc package
pkg1=wget
pkg2=curl
pkg3=mtr
pkg4=httpd
if yum list installed $pkg1 > /dev/null
then
echo "$pkg1 da duoc cai dat"
else
echo "$pkg1 dang duoc cai dat"
yum install -y $pkg1 > /dev/null
echo "$pkg1 da duoc cai dat thanh cong"
fi
if yum list installed $pkg2 > /dev/null
then
echo "$pkg2 da duoc cai dat"
else
echo "$pkg2 dang duoc cai dat"
yum install -y $pkg2 > /dev/null
echo "$pkg2 da duoc cai dat thanh cong"
fi
if yum list installed $pkg3 > /dev/null
then
echo "$pkg3 da duoc cai dat"
else
echo "$pkg3 dang duoc cai dat"
yum install -y $pkg3 > /dev/null
echo "$pkg3 da duoc cai dat thanh cong"
fi
if yum list installed $pkg4 > /dev/null
then
echo "$pkg4 da duoc cai dat"
else
echo "$pkg4 dang duoc cai dat"
yum install -y $pkg4 > /dev/null
echo "$pkg4 da duoc cai dat thanh cong"
fi
