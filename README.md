Installation Guide:

docker pull ubuntu:latest

docker run -it --name ubuntu-dev ubuntu:latest

docker ps -a

docker start ubuntu-dev

docker exec --it ubuntu-dev /bin/bash

apt update
apt install -y git cmake unzip libtomcrypt-dev libtommath-dev build-essential autoconf libtool bison flex libncurses5-dev libreadline-dev zlib1g-dev libicu-dev libedit-dev gdb

cd /root

git clone https://github.com/FirebirdSQL/firebird.git

cd firebird

./autogen.sh

./configure --prefix=/root/project/firebird CXXFLAGS="-g -O0" CFLAGS="-g -O0"

open /firebird in VSCode, open launch.json and replace with the following code 
{
  "version": "0.2.0",
  "configurations": [
    {
      "name": "Attach to Firebird",
      "type": "cppdbg",
      "request": "attach",
      "program": "/root/project/firebird/bin/firebird",
      "processId": "${command:pickProcess}",
      "MIMode": "gdb",
      "miDebuggerPath": "/usr/bin/gdb",
      "cwd": "${workspaceFolder}",
      "setupCommands": [
        { "text": "-enable-pretty-printing" }
      ],
      "sourceFileMap": {
        "/root/src": "/root/firebird/src" // Adjust this mapping
      }
    }
  ]
}

make

make install

After installation:
/root/project/firebird/bin/fbguard -daemon
/root/project/firebird/bin/isql



