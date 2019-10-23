#!bin/bash
echo "Bat dau tao khoa ssh"
echo "Xin moi nhap ten key:"
read -e id_rsa
if [ -e $HOME/.ssh/$id_rsa ] #check file da ton tai chua
then
	echo "Da co file trung ten, ghi de ko (y/n)"
	read -e check
		if [ $check == y ]
        then
        rm -rf $HOME/.ssh/$id_rsa
        elif [ $check == n ]
        then
        echo "Chon ten khac"
        read -e id_rsa
        fi
fi
echo "Qua trinh tao khoa ssh dang duoc bat dau"
ssh-keygen -t rsa -N "" -f $HOME/.ssh/$id_rsa > /dev/null
echo "Qua trinh tao khoa da duoc hoan tat, khoa duoc luu tai thu muc $HOME/.ssh"
echo "Nhap ten user muon ssh"
read -e user
echo "Nhap dia chi server"
read -e addr
ssh-copy-id -o "StrictHostKeyChecking no" -i ~/.ssh/$id_rsa $user@$addr
echo "Nhap ssh -i ~/.ssh/$id_rsa $user@$addr de login"