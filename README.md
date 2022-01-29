# linux-note

主要是紀錄一些 linux 的指令📝

( 本篇文章會持續更新:smile: )

## cd

切換到家目錄 `~`

```cmd
cd ~
```

切換到根目錄 `/`

```cmd
cd /
```

回到上層目錄

```cmd
cd ..
```

移動路徑到上一個所在的路徑 (可以快速切換兩個路徑, 很方便:smile:)

```cmd
cd -
```

## man

線上說明手冊 ( man page )

```cmd
man ls
```

![alt tag](https://i.imgur.com/3DDi208.png)

也可以使用

```cmd
ls --help
```

![alt tag](https://i.imgur.com/ZSZjuVC.png)

## pwd

查看目前的路徑

```cmd
pwd
```

## ls

[Youtube Tutorial - Linux 指令教學 - ls](https://youtu.be/3Zy1AWuDUHE)

列出檔案

```cmd
ls -l
```

`-l` 顯示詳細的資訊 ( 檔案權限 )。

也等於直接輸入 (L 的小寫)

```cmd
ll
```

在 Linux 中，檔案都擁有四種權限

* 可讀取 ( r，Readable )，用數字 4 表示。

* 可寫入 ( w，writable )，用數字 2 表示。

* 可執行 ( x，eXecute )，用數字 1 表示。

* 無權限 ( - )，用數字 0 表示。

為了更清楚，我把它整理成表格:yum:

|     字元     | 權限分數 |
|:------------:|:--------:|
|   r (read)   |     4    |
|   w (write)  |     2    |
|  x (execute) |     1    |
|    - 無權限  |     0    |

如下圖所示，

![alt tag](https://i.imgur.com/AzfYBhf.png)

接著說明裡面每一欄的意思，

![alt tag](https://i.imgur.com/3TMcAtC.png)

* 第一欄 ( 圖上編號 1 )，使用者權限。

由 10 個字元組成，

第一個字元代表檔案型態 (`-` 為檔案，`d` 為目錄，`l` 為連結檔案 )。

第二、三、四個字元 表示檔案擁有者的存取權限。

第五、六、七個字元 表示檔案擁有者所屬群組成員的存取權限。

第八、九、十個字元 表示其他使用者的存取權限。

來看一個例子，drwxr-xr-x，

代表它是一個目錄，

擁有者具備讀、寫、執行權限，

所屬群組只擁有讀、執行權限，

其他使用者只擁有讀、執行權限。

為了更清楚，我把它整理成表格:yum:

|                |        擁有者        |      所屬群組      |     其他使用者     |
|----------------|:--------------------:|:------------------:|:------------------:|
|        d       |          rwx         |         r-x        |         r-x        |
| 代表是一個目錄 | 具備讀、寫、執行權限 | 只擁有讀、執行權限 | 只擁有讀、執行權限 |

它的權限分數是 755

|  身份  	| 權限 	|   分數   	|
|:------:	|:----:	|:--------:	|
|  owner 	|  rwx 	| 4+2+1 =7 	|
|  group 	|  r-x 	| 4+0+1 =5 	|
| others 	|  r-x 	| 4+0+1 =5 	|

* 第二欄 ( 圖上編號 2 )，檔案數量。

* 第三欄 ( 圖上編號 3 )，擁有者。

* 第四欄 ( 圖上編號 4 )，群組。

* 第五欄 ( 圖上編號 5 )，檔案大小。

* 第六欄 ( 圖上編號 6 )，檔案建立時間。

* 第七欄 ( 圖上編號 7 )，檔案名稱。

ls 使用時間排序

```cmd
ls -t
```

列出特定檔案 ( 列出為 .py 的檔案 )

```cmd
ls *.py
```

`-h` 參數，使用 KB、MB、GB 單位顯示檔案或目錄大小。

```cmd
ls -l -h
```

顯示全部的檔案 (包含隱藏檔)

```cmd
ls -a
```

也可以使用

```cmd
ls -al
```

可以直接列出資料夾內的內容

```cmd
ls Downloads
```

像是在 home 底下, 直接列出 Downloads 內容

![alt tag](https://i.imgur.com/Dal7aSn.png)

sort

```cmd
ls -S
```

將輸出結果 stdout 寫到文件裡, 可使用 redirect `>` (螢幕上不會顯示)

```cmd
ls -lS > file.txt
```

## tee

同時將輸出結果 stdout 寫到文件裡以及顯示在螢幕上 (直接覆寫掉 file.txt)

```cmd
ls | tee file.txt
```

同時將輸出結果 stdout 寫到文件裡以及顯示在螢幕上 (附加在 file.txt 之後)

```cmd
ls | tee -a file.txt
```

##  touch

很常使用拿來建立空檔案

```cmd
touch file.py
```

也可以透過這個方式一次建立多個空檔案 ( `file1.py` ~ `file1.py`)

```cmd
touch file{1..10}.py
```

## su

切換不同的 user

```cmd
su <username>
```

## sudo

增加新的 user

```cmd
sudo useradd <username>
```

設定 user 的 password

```cmd
sudo passwd <username>
```

刪除 user

```cmd
sudo userdel <username>
```

增加新的 group

```cmd
sudo groupadd <groupname>
```

刪除 group

```cmd
sudo groupdel <groupname>
```

增加 user 到 group 中

```cmd
sudo usermod -g <groupname> <username>
```

查看所有 user

```cmd
sudo cat /etc/passwd
```

查看所有 group

```cmd
sudo cat /etc/group
```

不知道大家有沒有這個困擾, 就是每次都要打上自己的密碼很麻煩:expressionless:

這邊提供一個方法給各位, 但還是要小心一點, 就是 `-S` 這個指令.

```text
The -S (stdin) option causes sudo to read the password from
the standard input instead of the terminal device.
```

簡單說, 就是先打上你自己的密碼, 這樣就不用再打一次了, 以下舉例

```cmd
echo YourPwd | sudo -S groupadd <groupname>
```

## chmod

[Youtube Tutorial - Linux 教學 - chmod](https://youtu.be/qwk4Pzgtf2I)

chmod 為 change mode 的縮寫.

改變檔案權限

```cmd
chmod XXX filename
```

舉個例子，將權限設為 rw-rw-r--，

|  身份  	| 權限 	|   分數   	|
|:------:	|:----:	|:--------:	|
|  owner 	|  rw- 	| 4+2+0 =6 	|
|  group 	|  rw- 	| 4+2+0 =6 	|
| others 	|  r-- 	| 4+0+0 =4 	|

```cmd
chmod 664 README.md
```

常用修改權限的指令

```cmd
# 只有擁有者 owner 有讀和寫的權限
sudo chmod 600 ×××
```

```cmd
# 擁有者 owner 有讀和寫的權限，group，others 只有讀的權限
sudo chmod 644 ×××
```

```cmd
# 擁有者 owner 有讀和寫以及執行的權限
sudo chmod 700 ×××
```

```cmd
# 擁有者 owner，group，others 都有讀和寫的權限
sudo chmod 666 ×××
```

```cmd
# 擁有者 owner，group，others 都有讀和寫以及執行的權限，基本上就是全開
sudo chmod -R 777 xxx
```

`-r` `-R` 代表 recursive 遞迴 ( 目錄底下所以檔案包含子目錄都會變更 )，

還有一種方法是使用 符號 來改變權限，

在介紹之前，先看下方的表格 :wink:

|       | u = user  |          |             |              |
|-------|-----------|----------|-------------|--------------|
|       | g = group | + (增加) | r = read    |              |
| chmod |           | - (移除) | w = write   | 檔案或資料夾 |
|       | o = other | = (設定) | x = execute |              |
|       | a = all   |          |             |              |

舉個例子，將 hello 權限設為 rw-rw-r--，

|  擁有者(u)  	| 所屬群組(g) 	|   其他使用者(o)   	|
|:------:	|:----:	|:--------:	|
|  rw- 	|  rw- 	| r-- 	|

```cmd
chmod ug=rw,o=r hello
```

![alt tag](https://i.imgur.com/QgNuNel.png)

再舉個例子，將 hello 權限設為 rwxr-xr–-，

```cmd
chmod u=rwx,g=rx,o=r hello
```

![alt tag](https://i.imgur.com/WlX8wPL.png)

接著假設我希望把 可執行的權限(x) 加上去 (全部人及群組都加上)

```cmd
chmod a+x hello
```

![alt tag](https://i.imgur.com/KLiwPXX.png)

移除所有人 可執行的權限(x)

```cmd
chmod a-x hello
```

你會發現大家的 可執行的權限(x) 都消失了

![alt tag](https://i.imgur.com/O8gh3Is.png)

相信經過這一連串的練習，大家肯定了解了，

如果不懂，多看幾遍:satisfied:

## chown

修改檔案或目錄的擁有者與群組。

修改檔案或目錄的擁有者

```cmd
# 將 README.md ( 檔案 ) 的擁有者改為 twtrubiks ( 使用者 )
chown twtrubiks README.md
```

修改檔案或目錄的群組

```cmd
# 將 README.md ( 檔案 ) 的群組改為 twtrubiksgroup ( 群組 )
chown :twtrubiksgroup README.md
```

同時修改檔案或目錄的擁有者和群組

```cmd
# 將 README.md ( 檔案 ) 的擁有者改為 twtrubiks ( 使用者 ) 以及
# 將 README.md ( 檔案 ) 的群組改為 twtrubiksgroup ( 群組 )
chown twtrubiks:twtrubiksgroup README.md
```

## ln

[Youtube Tutorial - Linux 指令教學 - ln (Symbolic Link)](https://youtu.be/jdZsO2GAf2I)

有兩種, 分別為 hard link 和 Symbolic link ( soft link ),

先介紹 hard link，注意，hard link not allowed for directory。

```cmd
ln /home/twtrubiks/Downloads/odoo-git/README.md
```

![alt tag](https://i.imgur.com/ioJXBRw.png)

hard link 特性為不管刪除哪一個檔案，檔案都會被保留。除非你把最後一個檔案也刪除，

換個方式說，一個檔案的 hard link 和本來的檔案其實沒有任何實質上的區別。

hard link 不允許資料夾，只允許檔案。

symbolic link，也稱 soft link，基本上它類似於 Windows 中的捷徑:smile:

```cmd
ln -s /home/twtrubiks/Downloads/odoo-git/ dir-link
```

![alt tag](https://i.imgur.com/JGhlQZd.png)

當某個檔案的的本體被刪除後，它的 symbolic link 就無法讀取到這個檔案了，

一個檔案的 symbolic link 和檔案的本體是不同的兩個東西。

symbolic link 允許檔案和資料夾。

## zip unzip

zip 3.0 已經會保存檔案的 permissions and ownership.

```cmd
sudo apt-get install zip unzip
```

zip

```cmd
zip -r <壓縮後的檔名> <壓縮的檔案>
zip -r file.zip file
```

unzip

```cmd
unzip <解壓縮的檔案> -d <解壓縮的目標資料夾>
unzip file.zip -d zip_extract
```

如果希望直接解壓縮到當前的目錄，可以直接使用 `.`

```cmd
unzip file.zip -d .
```

## tar

tar **會**保存檔案的 permissions and ownership.

壓縮 `.tar` format

```cmd
tar cvf filename.tar source-folder
```

解壓縮 `.tar` format

```cmd
tar xvf filename.tar
```

## unrar

```cmd
sudo apt-get install unrar
```

將 filename.rar 解壓縮到目錄底下

```cmd
unrar e filename.rar
```

列出 filename.rar 的資料

```cmd
unrar l filename.rar
```

測試 filename.rar 是否完整且正確

```cmd
unrar t filename.rar
```

## wget

下載工具

```cmd
sudo apt-get install wget
```

下載 URL 指令

```cmd
wget http://ftp.gnu.org/gnu/wget/wget-1.20.3.tar.gz
```

指定檔名，請加上 `-O`

```cmd
wget -O wget.tar.gz http://ftp.gnu.org/gnu/wget/wget-1.20.3.tar.gz
```

## scp

全名為 Securely Copy,

這個方法適用於 Linux 和 Linux 之間互傳檔案，也適用於 Linux 和 Windows 之間互傳檔案，

假設，Linux ip 為 192.168.56.101，查看 ip 指令如下，

```cmd
ip addr show
```

![alt tag](https://i.imgur.com/AlAeRoD.png)

確認有安裝 openssh-server

```cmd
sudo apt-get install openssh-server
```

使用 `ssh localhsot` 測試

![alt tag](https://i.imgur.com/nYo5NNn.png)

一切正常之後。

從 Windows 上傳送檔案給 Linux ( ip 為 192.168.56.101 )，

在 Windows 上的 cmd 執行以下指令，

```cmd
scp -rp 檔案 linux的使用者@ip:目標路徑
```

`-r` 代表 recursive.

`-p` 代表 保存原始檔案的內容 (Preserves modification).

```cmd
scp -rp file twtrubiks@192.168.56.101:/home/twtrubiks
```

![alt tag](https://i.imgur.com/0nBrt00.png)

接下來，從 Linux 上拿檔案回 Windows

```cmd
scp -P 22 linux的使用者@ip:目標路徑 存放的目標位置
```

`-P` 代表明確指定連接的 port (remote host).

```cmd
scp -P 22 twtrubiks@192.168.56.101:/home/twtrubiks/linux_file.md .
```

`.` 代表當下目前路徑 ( 也可以指定其他的路徑 )。

![alt tag](https://i.imgur.com/aMnNlGI.png)

Linux 之間的傳送也是相同的道理:smile:

## mv

[Youtube Tutorial - Linux 指令教學 - mv](https://youtu.be/VhyzaEaGnL8)

move ( rename ) files，**移動檔案**或是**重新命名檔案**。

修改 資料夾 or 檔案 檔名

```cmd
mv folder folder-new
mv README.md README_MV.md
```

移動檔案

```cmd
mv README.md /examples
```

```cmd
mv file.md example/
```

其他的參數說明(參數可以多個一起使用)，

互動模式 , CLI 會詢問你是否 overwriting files

```cmd
mv -i source_file path_to_destination/
```

只更新來源資料夾和目的地不同的檔案

```cmd
mv -u source_file path_to_destination/
```

## rm

[Youtube Tutorial - Linux 指令教學 - rm](https://youtu.be/JqKjBZMXn_I)

刪除檔案

```cmd
rm file.md
```

刪除資料夾

```cmd
rm -rf mydir
```

`-r` 代表使用 recursive 遞迴刪除。 ( 會將目錄內所有檔案刪除 )

`-f` 代表強制刪除 ( 不會跳出警告 )。

或是使用 rmdir 指令，

```cmd
rmdir mydir_name
```

不過要注意，被移除的資料夾裡面必須是空的，否則回無法移除。

刪除特定的副檔名，

```cmd
rm -f *.zip
```

也可以這樣

```cmd
rm -f *demo.zip
```

## cp

[Youtube Tutorial - Linux 指令教學 - cp](https://youtu.be/ORl0YUGY728)

複製資料夾

```cmd
cp -r path_to_source/ path_to_destination/
```

`-r` `-R` 代表 recursive 遞迴，

如果 path_to_destination 不存在，會自動建立 ;

如果存在，則直接使用。

只想複製資料夾底下的全部內容，

```cmd
cp -r dir_1/. dir_2
cp -r dir_1/. .
```

`.` 代表資料夾內的東西，也可以代表目前所在的地方。

有時候會希望複製時可以保存當時的權限，所以會加上 `-p`。

```cmd
cp -r --preserve=all path_to_source/ path_to_destination/
```

`-p` `--preserve` 代表一同複製當下的權限以及擁有者之類的。

其他的參數說明(參數可以多個一起使用)，

互動模式 , CLI 會詢問你是否 overwriting files

```cmd
cp -i source_file path_to_destination/
```

不詢問 , 直接 overwriting files

```cmd
cp -n source_file path_to_destination/
```

只更新來源資料夾和目的地不同的檔案

```cmd
cp -u source_file path_to_destination/
```

印出資訊

```cmd
cp -v source_file path_to_destination/
```

## find

查詢檔案

找檔案或資料夾

```cmd
sudo find / -name "dir-name"
sudo find / -name "file-name"
sudo find / -name "*.conf"
```

在當前目錄下尋找檔名為 README.md

```cmd
find . -name README.md
```

## source

source 指令通常用於剛修改的初始化文件, 讓它立刻生效, 不必重開機(或登出再登入),

以下例子,

```cmd
source demo.sh
```

在當下的 shell 內去讀取, 執行 demo.sh, 而 demo.sh **需要**有執行權限

(執行權限代表 `chmod +x demo.sh`)

source 指令也可以簡寫為 `.`

```cmd
. demo.sh
```

## sh or bash

使用 `sh` or `bash`執行時, **不需要**有執行權限.

(執行權限代表 `chmod +x demo.sh`)

```cmd
sh demo.sh
bash demo.sh
```

## ./

直接使用 `./` 執行, **需要**有執行權限.

(執行權限代表 `chmod +x demo.sh`)

當你執行

```cmd
./demo.sh

chmod +x demo.sh
./demo.sh
```

你會發現跳出類似訊息 `bash: ./demo.sh: Permission denied`,

修正方法如下,

```cmd
chmod +x demo.sh
./demo.sh
```

## where

尋找路徑，

舉例，尋找 python3 路徑

```cmd
where python3
which python3
whereis python3
```

## tail

顯示檔案最後幾行內容

```cmd
tail README.md
```

一次顯示多個檔案

```cmd
tail README_1.md README_2.md
```

指定顯示檔案最後 N 行內容

```cmd
tail -n 5 README.md
```

```cmd
tail README.md -n 5
```

持續顯示更新內容，通常使用在 server 或看 log

```cmd
tail -f README.md
```

## head

既然有 tail, 肯定會有 head:smile:

```cmd
head text.py
```

預設顯示前 10 行資訊.

可以透過 `-n` 指令指定要顯示前 `n` 行

```cmd
head -n 3 text.py
```

## file

檢查檔案類型

```cmd
file README.md
```

## cat

將檔案內容顯示在 terminal 上

```cmd
cat README.md
```

顯示行數

```cmd
cat -n README.md
```

cat 也可以寫入檔案

```cmd
cat <<EOT >> hello_4.txt
line 1
line 2
line 3
EOT
```

## clear

clear the terminal screen ， 快捷鍵為 Ctrl+L

```cmd
clear
```

## grep

```cmd
# 格式
grep match_pattern file_name
```

```cmd
# 格式
grep "search name" README.md
```

也可以一次搜尋多個檔案

```cmd
grep "name" README_1.md README_2.md
```

也可以使用 萬用字元 `*`

```cmd
grep "print" *.py
```

搜尋當下目錄資料夾內容

```cmd
grep -r "search name" .
```

case insensitive case (不區分大小寫)

```cmd
grep -i "name" README_1.md
```

顯示行數

```cmd
grep -n "name" README_1.md
```

## sed

這個指令可以達到快速搜尋, 取代, 刪除文字,

sed 主要是針對**行**進行處理, 然後處理的不是原文件, 而是複製出來的文件.

語法

```cmd
sed -i '/匹配字串/d' textfile
```

`-i` 加上這個才會寫入你的 textfile, 不然只會顯示在 terminal 上.

刪除 empty lines

```cmd
sed -i '/^$/d' textfile
```

刪除有數字 7 的行數

```cmd
sed -i '/7/d' textfile
```

刪除第一到第五行

```cmd
sed -i '1,5d' textfile
```

刪除從 hello1 到 hello2 之間的所有行數

```cmd
sed -i '/hello1/, /hello2/d' textfile
```

替換語法

```cmd
sed -i 's/匹配字串/替代字串' textfile
```

將每行出現的第一個 a 替換成 A

```cmd
sed -i 's/a/A' textfile
```

將每行出現的全部的 a 替換成 A

```cmd
sed -i 's/a/A/g' file
```

`g` 代表替換所有匹配字串

## awk

這個指令是一個非常強大的文字分析工具

假設今天我們的輸出如下

![alt tag](https://i.imgur.com/GhPq6sZ.png)

把第 2,3,5,9 列輸出

```cmd
ll | awk '{print $2,$3,$5,$9}'
```

![alt tag](https://i.imgur.com/o1exYCq.png)

如果覺得醜, 可以用 printf 來排版

```cmd
ll | awk '{printf "%-5s %-5s %-5s %-5s\n", $2,$3,$5,$9}'
```

![alt tag](https://i.imgur.com/9RQj28o.png)

接過試著來過濾資料,

把 權限分數(第2列)分數是 2 以及 第3列是 twtrubiks 的取出來

```cmd
ll | awk '$2 == "2" && $3 == "twtrubiks" {print $0}'
```

`$0` 代表整行的所有內容.

![alt tag](https://i.imgur.com/Il9jGFp.png)

還可以進行統計,

把 權限分數(第2列) 的分數進行 sum (排除 total)

先排除掉第一列是 total 字串的資料,

my_sum 是我們定義的變數.

```cmd
ll | awk '$1 != "total" {my_sum+=$2} END{print my_sum}'
```

![alt tag](https://i.imgur.com/o3yXZnT.png)

也可以撰寫 if 邏輯,

把 權限分數(第2列)的分數為 3 的過濾出來,

接著印出目前行數, 以及把第9列的檔案名稱轉為大寫

```cmd
ll | awk '{if ($2 == "3") print NR, toupper($9)}'
```

NR 代表 Display Line Number.

![alt tag](https://i.imgur.com/dzlbMAA.png)

## mkdir

建立資料夾

```cmd
mkdir -p dir1/dir2
```

`-p` `--parents` 代表自動建立上層目錄，如果目錄已存在則不會發生錯誤。

## kill

強制停止程式執行.

需要先查到程式的 PID, 使用方法如下,

```cmd
kill -9 PID
```

`-9` 立刻強制停止程式執行

## killall

killall 和 kill 的一個差別是可以使用程式名稱,

不需要先找到程式的 PID,

例如想要強制停止 vlc

```cmd
killall vlc
```

## history

歷史輸入的指令

```cmd
history
```

```cmd
history | less
```

![alt tag](https://i.imgur.com/0YKqS3Y.png)

假設今天我不想打指令, 可以直接輸入 `!`+ 數字, 會自動執行該指令.

```cmd
!1848
```

再顯示一次最後輸入的指令 (建議加上 sudo)

```cmd
!!
```

也可以搭配 grep,

假如我想要找到歷史輸入過 `git` 的指令, 這時候可以使用以下的指令

```cmd
history | grep git
```

如果我不想一次顯示全部, 可以再搭配 less

```cmd
history | grep git | less
```

## echo

在 shell 中印出 shell 的值，

設定 EDITOR

```cmd
export EDITOR=vim
```

查看目前的 EDITOR，

```cmd
echo $EDITOR
```

查看目前的 shell，

```cmd
echo $SHELL
```

echo 也可以寫入檔案，

方法一

```cmd
echo "line 1" >> hello_1.txt
```

方法二 ( 寫入多行 )

```cmd
echo "line 1
line 2" >> hello_2.txt
```

方法三 ( 寫入多行 )

```cmd
{
    echo 'line1;'
    echo 'line2;'
} >> hello_3.txt
```

## du

[Youtube Tutorial - Linux 指令教學 - du(Disk Usage)](https://youtu.be/JZZoJnasnHE)

du 這個指令是 Disk Usage 的縮寫,

在開始介紹 du 之前, 先來看一個例子,

使用 `ls -l -h` 觀察 debian 資料夾

![alt tag](https://i.imgur.com/lXgxQop.png)

但是如果你進到資料夾裡面, 你會發現它明明有 17GB,

可是為什麼在資料夾外層看的時候卻只有 4KB:question:

![alt tag](https://i.imgur.com/eOTKWJj.png)

原因是 `ls -l -h` 不會顯示資料夾實際的大小, 只會顯示所謂的 meta information,

所以, 如果你要看實際的大小, 比較好的方法是使用接下來要介紹的 `du` 指令:smile:

查看 du 指令說明

```cmd
du --help
```

![alt tag](https://i.imgur.com/IQLpqnC.png)

```cmd
-s, --summarize       display only a total for each argument
                      (Equivalent to -d 0)

-h, --human-readable  print sizes in human readable format (e.g., 1K 234M 2G)
    --inodes          list inode usage information instead of block usage

-c, --total           produce a grand total

-d, --max-depth=N     print the total for a directory (or file, with --all)
                      only if it is N or fewer levels below the command
                      line argument;  --max-depth=0 is the same as --summarize


-a, --all             write counts for all files, not just directories
    --apparent-size   print apparent sizes, rather than disk usage; although
                      the apparent size is usually smaller, it may be
                      larger due to holes in ('sparse') files, internal
                      fragmentation, indirect blocks, and the like
```

以下兩個指令功能是相同的

```cmd
du -sh *
du --summarize --human-readable *
```

使用剛剛的那個例子, 在資料夾的外層就能看到實際的資料夾大小

![alt tag](https://i.imgur.com/hHjxXDx.png)

也可以搭配 `-d` 使用, 資料夾的層數, 看下面的例子你就會懂了

```cmd
du -d 2 -h
```

![alt tag](https://i.imgur.com/NdbqvSz.png)

## truncate

[Youtube Tutorial - Linux 指令教學 - truncate](https://youtu.be/w2pwD1AOhPI)

Shrink or extend the size of each FILE to the specified size.

truncate 指令可以將一個檔案縮小或是增加大小.

開始介紹這個指令前, 先來看看適用的情境:smile:

有時候我們可能會希望把一個檔案的大小歸 0, 也就是將檔案的內容全部刪除,

但是要保留檔案, 這時候就很適合使用這個指令:smirk:

那你可能會問我, 為什麼不直接刪除檔案再建立一個一模一樣的就好:question:

原因很簡單, 在 linux 的世界中, 檔案是有權限的, 所以你還要去注意新建立

出來的檔案, 權限是否和之前的一模一樣( 否而可能會導致錯誤 ), 所以比較簡單

的方法會是使用 truncate 這個指令, 它將只會清除內容 ( 檔案大小為 0 ),

其餘的都保持原來的狀態。

查看 truncate 指令說明,

```cmd
truncate --help
```

![alt tag](https://i.imgur.com/rOXR79N.png)

```cmd
Mandatory arguments to long options are mandatory for short options too.
-c, --no-create        do not create any files
-o, --io-blocks        treat SIZE as number of IO blocks instead of bytes
-r, --reference=RFILE  base size on RFILE
-s, --size=SIZE        set or adjust the file size by SIZE bytes
    --help     display this help and exit
    --version  output version information and exit

SIZE may also be prefixed by one of the following modifying characters:
'+' extend by, '-' reduce by, '<' at most, '>' at least,
'/' round down to multiple of, '%' round up to multiple of.
```

使用以下的範例來說明,

假設現在有一個 `demo.txt` 的檔案 (如下)

![alt tag](https://i.imgur.com/nWoxmhn.png)

使用 truncate 將 `demo.txt` 放大到 1M,

```cmd
truncate -s 1M demo.txt
```

![alt tag](https://i.imgur.com/jeZ6Rkp.png)

注意 `du -ah` 是顯示 apparent sizes (不是 disk usage ), 所以大小不會改變.

如果你去打開 `demo.txt`, 你會發現被塞了很多東西, 因為大小要變成 1M:smile:

![alt tag](https://i.imgur.com/mgQNkNn.png)

相反的, 現在使用 truncate 將 `demo.txt` 縮小到 0,

![alt tag](https://i.imgur.com/9czKNL5.png)

如果你去打開 `demo.txt`, 你會發現裡面的資料都消失了.

![alt tag](https://i.imgur.com/vmLwz96.png)

truncate 這個指令就非常適合去清除 log, 將 log 大小歸 0, 其餘保持原樣.

清空所有日誌文件

```cmd
sudo truncate -s 0 /var/log/**/*.log
```

## 不用密碼遠端登入 Linux

### 方法一

先確認 Linux 上有 `.ssh` 資料夾，如果沒有，

請使用以下指令建立 ( 以及權限 )，

```cmd
mkdir -p ~/.ssh
chmod 700 ~/.ssh
```

每次遠端登入 Linux 都需要密碼很麻煩，有沒有可以透過其他的方式不要輸入密碼:question:

有，先在本機電腦使用 `ssh-keygen` 產生金鑰

```cmd
ssh-keygen
```

接著你會有兩把 key ,

id_rsa.pub：公開金鑰（public key）: 要放在遠端的 Linux 伺服器上。

id_rsa：私密金鑰（private key）: 自己保護好，等同於你的 Linux 密碼。

先把自己本機 `id_rsa.pub` 傳到遠端的 Linux server 上，

接著在 Linux 上執行以下指令

( 把公開金鑰放到 `~/.ssh/authorized_keys` )

```cmd
cat id_rsa.pub >> ~/.ssh/authorized_keys
```

讓我們來測試看看吧:smile:

`ssh twtrubiks@192.168.56.101`

![alt tag](https://i.imgur.com/97ndrP8.png)

不用輸入密碼就可以登入了:thumbsup:

### 方法二

也可以透過 `ssh-copy-id` 來完成,

```cmd
ssh-copy-id -i ~/.ssh/id_rsa.pub twtrubiks@192.168.56.101
```

![alt tag](https://i.imgur.com/eR5TIJ3.png)

其實不管是方法一還是方法二, 都只是把 key 加入 `/home/<user>/.ssh`

裡的 `authorized_keys` 而已:smile:

![alt tag](https://i.imgur.com/j4BRI1J.png)

## root 使用者登入遠端 Linux

注意, 通常不會這樣做:exclamation:

雖然這個方法可以比較危險，但我還是說明一下:joy:

先設定 root 密碼，執行以下指令

```cmd
sudo passwd root
```
![alt tag](https://i.imgur.com/dsSrBJX.png)

再使用 `su -` 測試 root 密碼

![alt tag](https://i.imgur.com/nmU9cgk.png)

測試完成後，再執行 `ssh root@192.168.56.101`

![alt tag](https://i.imgur.com/BF4JWnO.png)

你會發現一直出現 Permission denied, please try again.

這時候要到 Linux 上修改 root 的 ssh 設定，

```cmd
sudo vim /etc/ssh/sshd_config
```

找到 PermitRootLogin without-password

![alt tag](https://i.imgur.com/NO85xui.png)

修改成 PermitRootLogin yes

![alt tag](https://i.imgur.com/xpyfpwW.png)

最後記得一定要重新啟動 sshd 讓它生效 (或是重開機)

```cmd
systemctl restart sshd
```

成功使用 root 登入了:satisfied:

![alt tag](https://i.imgur.com/Au4wt32.png)

## 正確保護 server

比較安全的作法通常是關閉 `PermitRootLogin` 以及 `PasswordAuthentication`,

然後只啟用 `PubkeyAuthentication` 的方式, 但這邊要注意, 一定要把你的 key 放到

server 上, 否則如果設定完不小心退出, 就很麻煩:expressionless:

( 因為不能用密碼登入, 又忘記將 key 放到 server 中 )

修改

```cmd
sudo vim /etc/ssh/sshd_config
```

禁止 root 登入, 將 `PermitRootLogin` 設為 `no`,

![alt tag](https://i.imgur.com/W6KBiXS.png)

禁止使用 password 登入, 將 `PasswordAuthentication` 設為 `no`,

![alt tag](https://i.imgur.com/L9WPRq5.png)

允許 `PubkeyAuthentication`, 設為 `yes`

![alt tag](https://i.imgur.com/iYyaAQ8.png)

補充, 還有一種是使用 PAM Authentication `UsePAM` ( AWS 就是使用這種方式 )

![alt tag](https://i.imgur.com/g3MdnKC.png)

如同說明, 如果希望只使用 PAM Authentication, 也可以把 `ChallengeResponseAuthentication` 設為 `no`.

最後記得重新啟動 sshd 讓它生效 (或是重開機)

```cmd
systemctl restart sshd
```

## 其他資訊

系統訊息

```cmd
uname -a
```

查看 cpu

```cmd
cat /proc/cpuinfo
```

查看全部的 ram 大小

```cmd
grep MemTotal /proc/meminfo
```

查看可用的 ram

```cmd
grep MemFree /proc/meminfo
```

也可以使用

```cmd
free -m
```

查看硬碟空間 ( disk free space, Human Readable )

```cmd
df -h
```

所有硬碟的訊息 ( List Drives and Mounts )

```cmd
lsblk
```

顯示所有裝置設備的資訊 ,UUID

```cmd
blkid
```

![alt tag](https://i.imgur.com/8a6V7fq.png)

目前硬碟 mount 狀態 (開機自動掛載)

```cmd
cat /etc/fstab
```

![alt tag](https://i.imgur.com/79WxI5w.png)

查看所有 pci，

```cmd
lspci
```

查看所有 usb，

```cmd
lsusb
```

也可以搭配 grep 搜尋，只搜尋包含 VirtualBox 的內容，

```cmd
lsusb | grep VirtualBox
```

查看 ip，

```cmd
ip a
```

external ip Address ( 對外的 ip )，`ifconfig.me` 是一個網站，

```cmd
curl ifconfig.me
```

查看電腦目前資訊，CPU RAM 等等

```cmd
top
```

推薦 `htop` ( 資訊更清楚 ), 建議參考 [htop-tutorial](https://github.com/twtrubiks/linux-note/tree/master/htop-tutorial) - htop tutorial:thumbsup:

透過 xrandr 修改螢幕的亮度，

先查看螢幕的 name，

```cmd
xrandr | grep " connected" | cut -f1 -d " "
```

設定亮度 ( 0 - 1 )，

```cmd
xrandr --output DP-1 --brightness 0.7
```

透過 systemd-analyze 查看 Linux 啟動時間

```cmd
systemd-analyze
```

查看細節

```cmd
systemd-analyze blame
```

###  如何進入 tty 介面

有時候開機時可能因為驅動沒裝, 導致卡在黑屏的畫面,

這時候就可以進入 tty 介面安裝驅動(需要的東西),

進入 tty 快捷建 `Ctrl+Alt+F2`

退出 tty 快捷建 `Ctrl+Alt+F7` 或 `Ctrl+Alt+(F2/F3/F4)`

### swap

如果你的本機 ram 夠大, 可以考慮把它關掉,

(有些 distro 預設是打開的 )

關閉 swap

```cmd
sudo swapoff -a
```

打開 swap

```cmd
sudo swapon -a
```

以下指令可以幫你找出哪些程式用了多少 swap

```cmd
(echo "COMM PID SWAP"; for file in /proc/*/status ; do awk '/^Pid|VmSwap|Name/{printf $2 " " $3}END{ print ""}' $file; done | grep kB | grep -wv "0 kB" | sort -k 3 -n -r) | column -t
```

![alt tag](https://i.imgur.com/uibxLSu.png)

## install packages

install

```cmd
sudo apt-get install xxx
```

如果只有 `.deb` 檔案, 可以使用以下的方式

```cmd
sudo apt install ./xxx.deb
```

update list ( 更新 packages 的最新資訊及列表 )

```cmd
sudo apt-get update
```

upgrade ( 更新軟體到最新的版本 )

```cmd
sudo apt-get upgrade
```

只更新特定的軟體, 舉例 vivaldi,

先更新再安裝就是更新軟體的意思,

```cmd
sudo apt update && sudo apt install vivaldi-stable
```

remove

```cmd
sudo apt-get --purge autoremove xxxx
```

清理不需要的 packages ( `.deb` )

```cmd
sudo apt autoclean
```

清除不需要的依賴

```cmd
sudo apt autoremove
```

## ppa add/remove

add

```cmd
sudo apt-add-repository ppa:xxxx
sudo apt update
```

remove

```cmd
sudo add-apt-repository -r ppa:xxxx
sudo apt update
```

## 無法進入 bios

```cmd
sudo vim /etc/default/grub
```

你應該會看到類似的畫面

```text
GRUB_DEFAULT="0"
GRUB_TIMEOUT_STYLE="hidden"
GRUB_TIMEOUT=10   <<<<<<
GRUB_DISTRIBUTOR="`lsb_release -i -s 2> /dev/null || echo Debian`"
GRUB_CMDLINE_LINUX_DEFAULT="quiet splash usbcore.autosuspend=-1"
GRUB_CMDLINE_LINUX=""
```

將 GRUB_TIMEOUT 的時間改長一點, 因為有可能是太快了, 導致來不及按:disappointed_relieved:

也請記得要再執行以下的指令更新

```cmd
sudo update-grub
```

## remove snap

在 ubuntu 中, 預設會幫你安裝 snap, 但有些人不太喜歡,

因為他是私人公司為維護的:smile:

以下附上移除 snap 指令,

```cmd
sudo rm -rf /var/cache/snapd/
sudo apt autoremove --purge snapd gnome-software-plugin-snap
rm -rf ~/snap
```

## remove ubuntu 不需要的軟體

使用 ubuntu 18.04 當範例

```cmd
sudo apt purge deja-dup thunderbird rhythmbox ubuntu-web-launchers whoopsie
```

`deja-dup` ubuntu 內建備份軟體.

`whoopsie` ubuntu 錯誤報告.

如果不小心刪除到依賴 (把 settings 刪除), 可使用以下指令將它裝回來

```cmd
sudo apt-get install gnome-control-center
```

## Linux 檔案系統(結構)

[Linux-File-System/Structure](https://github.com/twtrubiks/linux-note/tree/master/linux-file-system-structure)

## 更多文章

[zsh-tmux-tutorual](https://github.com/twtrubiks/linux-note/tree/master/zsh-tmux-tutorual) - 超好用 zsh 以及 tmux。

[zsh-powerlevel10k-tutorual](https://github.com/twtrubiks/linux-note/tree/master/zsh-powerlevel10k-tutorual) - zsh 搭配 Powerlevel10k, 超漂亮 terminal。

[vim-shortcuts](https://github.com/twtrubiks/linux-note/tree/master/vim-shortcuts) - 紀錄 vim 快捷鍵

[imwheel-tutorual](https://github.com/twtrubiks/linux-note/tree/master/imwheel-tutorual) - 改善 linux 滑鼠滾動問題。

[shutter-tutorual](https://github.com/twtrubiks/linux-note/tree/master/shutter-tutorual) - Shutter is an excellent image capture tool.

[systemctl-tutorial](https://github.com/twtrubiks/linux-note/tree/master/systemctl-tutorial) - systemctl 命令是系統服務管理指令

[crontab-tutorual](https://github.com/twtrubiks/linux-note/tree/master/crontab-tutorual) - Linux Crontab

[mount-disks-at-system-startup-on-ubuntu](https://github.com/twtrubiks/linux-note/tree/master/mount-disks-at-system-startup-on-ubuntu)

[chinese-input-methods-on-ubuntu](https://github.com/twtrubiks/linux-note/tree/master/chinese-input-methods-on-ubuntu) - ubuntu 如何安裝中文輸入法

[hime-tutorial](https://github.com/twtrubiks/linux-note/tree/master/hime-tutorial) - Linux 中更像微軟更好用的中文輸入法 hime

[gnome-tweaks](https://github.com/twtrubiks/linux-note/tree/master/gnome-tweaks) - Ubuntu 安裝 GNOME Tweak tool

[htop-tutorial](https://github.com/twtrubiks/linux-note/tree/master/htop-tutorial) - htop tutorial:thumbsup:

[neofetch-tutorial](https://github.com/twtrubiks/linux-note/tree/master/neofetch-tutorial) - command-line system information tool:thumbsup:

[copyq-tutorial](https://github.com/twtrubiks/linux-note/tree/master/copyq-tutorial) - 剪貼簿:thumbsup:

[krusader-tutorial](https://github.com/twtrubiks/linux-note/tree/master/krusader-tutorial) - file manager

[fail2ban-tutorial](https://github.com/twtrubiks/linux-note/tree/master/fail2ban-tutorial) - 讓 server 更安全:smile:

[how-to-change-login-lock-background-ubuntu](https://github.com/twtrubiks/linux-note/tree/master/how-to-change-login-lock-background-ubuntu) - 修改Ubuntu 登入/鎖屏時的背景

[grub-customizer-tutorial](https://github.com/twtrubiks/linux-note/tree/master/grub-customizer-tutorial) - 安裝 grub-customizer

[enable-ubuntu-remote-tutorial](https://github.com/twtrubiks/linux-note/tree/master/enable-ubuntu-remote-tutorial) - 如何在 ubuntu 啟用遠端桌面

[linux-nfs-server](https://github.com/twtrubiks/linux-note/tree/master/linux-nfs-server) - 如何在 ubuntu 啟用 NFS Server

## 狀況排除

[fix_could_not_get_lock_dpkg_ubuntu](https://github.com/twtrubiks/linux-note/tree/master/fix_could_not_get_lock_dpkg_ubuntu) - 修正 `E: Could not get lock /var/lib/dpkg/lock` Error

[fix_network_manager_bug_ubuntu_18_04](https://github.com/twtrubiks/linux-note/tree/master/fix_network_manager_bug_ubuntu_18_04) - 修正 ubuntu 18.04 網路連線設定遺失問題.

## 其他

[Windows -> Linux 優缺點](https://github.com/twtrubiks/linux-note/tree/master/linux-is-better-than-windows) - Windows -> Linux 優缺點

[ubuntu-18-04-on-Lenovo-X1-Carbon-6](https://github.com/twtrubiks/linux-note/tree/master/ubuntu-18-04-on-Lenovo-X1-Carbon-6)

[透過 VirtualBox 安裝 Ubuntu 19.10 （以及一些個人想法）](https://youtu.be/lI1EMwhW6lE)

[VirtualBox 6.1 Linux 安裝 Guest Addition - 全屏教學](https://youtu.be/PMw6FPtbbaU)

[alternative-software](https://github.com/twtrubiks/linux-note/tree/master/alternative-software) - windows -> Linux 替代軟體

[rclone-tutorial](https://github.com/twtrubiks/linux-note/tree/master/rclone-tutorial) - rclone 是一套很棒的文件同步管理工具

[stacer-tutorial](https://github.com/twtrubiks/linux-note/tree/master/stacer-tutorial) - Linux System Optimizer and Monitoring

[cmatrix-tutorial](https://github.com/twtrubiks/linux-note/tree/master/cmatrix-tutorial) - 超酷又超沒用的 cmatrix

[sl-tutorial](https://github.com/twtrubiks/linux-note/tree/master/sl-tutorial) - sl 火車開起來

[linux-tlp-tutorial](https://github.com/twtrubiks/linux-note/tree/master/linux-tlp-tutorial) - Linux Advanced Power Management

[speedtest-cli-tutorial](https://github.com/twtrubiks/linux-note/tree/master/speedtest-cli-tutorial) - Linux speedtest-cli tutorial

[gnirehtet-tutorial-tutorial](https://github.com/twtrubiks/linux-note/tree/master/gnirehtet-tutorial) - 透過電腦讓手機上網

[scrcpy-tutorial-tutorial](https://github.com/twtrubiks/linux-note/tree/master/scrcpy-tutorial) - 使用電腦控制手機

[variety-tutorual](https://github.com/twtrubiks/linux-note/tree/master/variety-tutorual) - variety 自動更換桌面

[arandr-tutorual](https://github.com/twtrubiks/linux-note/tree/master/arandr-tutorual) - arandr 設定多螢幕工具

[linux-virtualbox-ssh-tutorial](https://github.com/twtrubiks/linux-note/tree/master/linux-virtualbox-ssh-tutorial) - 在 Linux 中設定 VirtualBox 把玩 ssh

[linux-virtualbox-problem](https://github.com/twtrubiks/linux-note/tree/master/linux-virtualbox-problem) - 在 Linux 中設定 VirtualBox - 常見問題

[QEMU-KVM-tutorial](https://github.com/twtrubiks/linux-note/tree/master/QEMU-KVM-tutorial) - QEMU-KVM (效能速度比 virtualbox 更好)

[Linux 桌面環境 Desktop Environment](https://github.com/twtrubiks/linux-note/tree/master/linux-de)

[認識 Linux 發行版 distribution](https://github.com/twtrubiks/linux-note/tree/master/linux-distro)

[KDE setting](https://github.com/twtrubiks/linux-note/tree/master/kde-settings)

## Reference

* [Linux Command 命令列指令與基本操作入門教學](https://blog.techbridge.cc/2017/12/23/linux-commnd-line-tutorial/)

## Donation

文章都是我自己研究內化後原創，如果有幫助到您，也想鼓勵我的話，歡迎請我喝一杯咖啡:laughing:

綠界科技ECPAY ( 不需註冊會員 )

![alt tag](https://payment.ecpay.com.tw/Upload/QRCode/201906/QRCode_672351b8-5ab3-42dd-9c7c-c24c3e6a10a0.png)

[贊助者付款](http://bit.ly/2F7Jrha)

歐付寶 ( 需註冊會員 )

![alt tag](https://i.imgur.com/LRct9xa.png)

[贊助者付款](https://payment.opay.tw/Broadcaster/Donate/9E47FDEF85ABE383A0F5FC6A218606F8)

## 贊助名單

[贊助名單](https://github.com/twtrubiks/Thank-you-for-donate)

## License

MIT license
