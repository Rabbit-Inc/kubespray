Working with the kubespray repo
===============================

https://help.github.com/articles/syncing-a-fork/
https://help.github.com/articles/pushing-to-a-remote/
https://help.github.com/articles/dealing-with-non-fast-forward-errors/

git fetch upstream
git checkout master
git pull upstream master (this is supposed to merge too)
git merge upstream master

idk one of these I guess
git pull origin master

git checkout -b brandon/thing
git commit
git push -u -f origin brandon/inventory080818-2
git checkout master
git rebase -Xtheirs master



10090  git rebase master -X theirs
10095  git pull
10098  git checkout brandon/makesideclusterslikeprod
10100  git push
10101  git checkout master
10102  git fetch
10103  git pull --rebase origin master
10104  ls


Running Kubespray
===========================

ansible-playbook -i inventory/mycluster/hosts.ini cluster.yml -b -v  --private-key=~/.ssh/id_rsa.rabbit-prod-v20160119 --become

add in the new hosts to hosts.ini


Worker node setup
===============================
worker hosts need these dependencies

sudo mkdir -p /etc/apt/sources.list.d/; echo "deb https://apt.dockerproject.org/repo ubuntu-xenial main" | sudo tee /etc/apt/sources.list.d/docker.list

printf "nameserver 10.0.0.3 \nnameserver 10.0.0.4" | sudo tee /etc/resolv.conf /etc/resolvconf/resolv.conf.d/head
printf "nameserver 8.8.8.8 \nnameserver 8.8.4.4" | sudo tee /etc/resolv.conf /etc/resolvconf/resolv.conf.d/head

sudo apt-get update -y ; sudo apt-get upgrade -y; sudo apt-get install ceph-fs-common ceph-common python docker-engine -y
sudo apt-get update -y ; sudo apt-get upgrade -y; sudo apt-get install ceph-fs-common ceph-common python docker-engine -y --allow-unauthenticated

echo "ubuntu ALL=(ALL) NOPASSWD:ALL" | sudo tee /etc/sudoers.d/ubuntu;

mkdir -p /home/ubuntu/.ssh/; echo "ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQC3E7Y8mZjCAxn/HL6tyzGOhM+7keBpcMNPEZWve/mjbFEEUQI6IE1p7B4vp42Wj+Lek0XSBcaZDyuZJW2tNvpbJ3ZxHle+9afTJxd6DW2eVucZC6d2AiLmFRyVtYZwLwPHfcvYauEHQCquM7zxrB+hUZnVWeYMTJlLOCVBHrcxX9AvzLVLqzcaf2A72bgHLgSOjzHjifmM/Ze+9lLWHVuEMytcfg5tehv9jn4uccJupDAF85EH+PFHhUkzHQngZ9g8sqIBX0OZAlyhKCsp9wIYeCREM8J3kXiWbj3F9RK7Mg5AUGPKLJf7wiP5QsYr+AcUbz+ideLWrDD16KvgYw31 rabbit-prod-v20160119" | sudo tee /home/ubuntu/.ssh/authorized_keys

echo "net.ipv4.ip_forward = 1" | sudo tee /etc/sysctl.conf
sudo sysctl -w net.ipv4.ip_forward=1

DOUBLE CHECK THAT THERE IS NO SWAP

