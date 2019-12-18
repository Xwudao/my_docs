# Linux

## 备份压缩

### bunzip2

**功能说明：**.bz2文件的解压缩程序。
**语　　法：**bunzip2 -fkLsvV
**补充说明：**bunzip2可解压缩.bz2格式的压缩文件。bunzip2实际上是bzip2的符号连接，执行bunzip2与bzip2 -d的效果相同。
**参　　数：**
　-f或--force 　解压缩时，若输出的文件与现有文件同名时，预设不会覆盖现有的文件。若要覆盖，请使用此参数。 
　-k或--keep 　在解压缩后，预设会删除原来的压缩文件。若要保留压缩文件，请使用此参数。 
　-s或--small 　降低程序执行时，内存的使用量。 
　-v或--verbose 　解压缩文件时，显示详细的信息。 
　-l,--license,-V或--version 　显示版本信息。

### bzip2

**功能说明：**.bz2文件的压缩程序。
**语　　法：**bzip2 -cdfhkLstvVz --repetitive-fast[要压缩的文件]
**补充说明：**bzip2采用新的压缩演算法，压缩效果比传统的LZ77/LZ78压缩演算法来得好。若没有加上任何参数，bzip2压缩完文件后会产生.bz2的压缩文件，并删除原始的文件。
**参　　数：**
　-c或--stdout 　将压缩与解压缩的结果送到标准输出。 
　-d或--decompress 　执行解压缩。 
　-f或--force 　bzip2在压缩或解压缩时，若输出文件与现有文件同名，预设不会覆盖现有文件。若要覆盖，请使用此参数。 
　-h或--help 　显示帮助。 
　-k或--keep 　bzip2在压缩或解压缩后，会删除原始的文件。若要保留原始文件，请使用此参数。 
　-s或--small 　降低程序执行时内存的使用量。 
　-t或--test 　测试.bz2压缩文件的完整性。 
　-v或--verbose 　压缩或解压缩文件时，显示详细的信息。 
　-z或--compress 　强制执行压缩。 
　-L,--license,
　-V或--version 　显示版本信息。 
　--repetitive-best 　若文件中有重复出现的资料时，可利用此参数提高压缩效果。 
　--repetitive-fast 　若文件中有重复出现的资料时，可利用此参数加快执行速度。 
　-压缩等级 　压缩时的区块大小。

### gunzip(gnu unzip)

**功能说明：**解压文件。
**语　　法：**gunzip -acfhlLnNqrtvV[文件...] 或 gunzip -acfhlLnNqrtvV[目录]
**补充说明：**gunzip是个使用广泛的解压缩程序，它用于解开被gzip压缩过的文件，这些压缩文件预设最后的扩展名为".gz"。事实上gunzip就是gzip的硬连接，因此不论是压缩或解压缩，都可通过gzip指令单独完成。
**参　　数：**
　-a或--ascii 　使用ASCII文字模式。 
　-c或--stdout或--to-stdout 　把解压后的文件输出到标准输出设备。 
　-f或-force 　强行解开压缩文件，不理会文件名称或硬连接是否存在以及该文件是否为符号连接。 
　-h或--help 　在线帮助。 
　-l或--list 　列出压缩文件的相关信息。 
　-L或--license 　显示版本与版权信息。 
　-n或--no-name 　解压缩时，若压缩文件内含有远来的文件名称及时间戳记，则将其忽略不予处理。 
　-N或--name 　解压缩时，若压缩文件内含有原来的文件名称及时间戳记，则将其回存到解开的文件上。 
　-q或--quiet 　不显示警告信息。 
　-r或--recursive 　递归处理，将指定目录下的所有文件及子目录一并处理。 
　-S<压缩字尾字符串>或--suffix<压缩字尾字符串> 　更改压缩字尾字符串。 
　-t或--test 　测试压缩文件是否正确无误。 
　-v或--verbose 　显示指令执行过程。 
　-V或--version 显示版本信息。

### gzip(gnu zip)

**功能说明：**压缩文件。
**语　　法：**gzip -acdfhlLnNqrtvV-<压缩效率>[文件...] 或 gzip -acdfhlLnNqrtvV-<压缩效率>[目录]
**补充说明：**gzip是个使用广泛的压缩程序，文件经它压缩过后，其名称后面会多出".gz"的扩展名。
**参　　数：**
　-a或--ascii 　使用ASCII文字模式。 
　-c或--stdout或--to-stdout 　把压缩后的文件输出到标准输出设备，不去更动原始文件。 
　-d或--decompress或----uncompress 　解开压缩文件。 
　-f或--force 　强行压缩文件。不理会文件名称或硬连接是否存在以及该文件是否为符号连接。 
　-h或--help 　在线帮助。 
　-l或--list 　列出压缩文件的相关信息。 
　-L或--license 　显示版本与版权信息。 
　-n或--no-name 　压缩文件时，不保存原来的文件名称及时间戳记。 
　-N或--name 　压缩文件时，保存原来的文件名称及时间戳记。 
　-q或--quiet 　不显示警告信息。 
　-r或--recursive 　递归处理，将指定目录下的所有文件及子目录一并处理。 
　-S<压缩字尾字符串>或----suffix<压缩字尾字符串> 　更改压缩字尾字符串。 
　-t或--test 　测试压缩文件是否正确无误。 
　-v或--verbose 　显示指令执行过程。 
　-V或--version 　显示版本信息。 
　-<压缩效率> 　压缩效率是一个介于1－9的数值，预设值为"6"，指定愈大的数值，压缩效率就会愈高。 
　--best 　此参数的效果和指定"-9"参数相同。 
　--fast 　此参数的效果和指定"-1"参数相同。

### tar(tape archive)

**功能说明：**备份文件。
**语　　法：**tar -ABcdgGhiklmMoOpPrRsStuUvwWxzZ-C <目的目录>-F <Script文件>-L <媒体容量>-T <范本文件>-X <范本文件>--after-date=<日期时间>--backuup=<备份方式>--concatenate--delete--force-local--help--new-volume-script=<Script文件>--no-recursion--numeric-owner--posix--preserve-order--record-size=<区块数目>--remove-files--same-owner--totals--version[文件或目录...]
**补充说明：**tar是用来建立，还原备份文件的工具程序，它可以加入，解开备份文件内的文件。
**参　　数：**
  -A或--catenate   新增温暖件到已存在的备份文件。
  -b<区块数目>或--blocking-factor=<区块数目>   设置每笔记录的区块数目，每个区块大小为12Bytes。
  -B或--read-full-records   读取数据时重设区块大小。
  -c或--create   建立新的备份文件。
  -C<目的目录>或--directory=<目的目录>   切换到指定的目录。
  -d或--diff或--compare   对比备份文件内和文件系统上的文件的差异。
  -f<备份文件>或--file=<备份文件>   指定备份文件。
  -F<Script文件>或--info-script=<Script文件>   每次更换磁带时，就执行指定的Script文件。
  -g或--listed-incremental   处理GNU格式的大量备份。
  -G或--incremental   处理旧的GNU格式的大量备份。
  -h或--dereference   不建立符号连接，直接复制该连接所指向的原始文件。
  -i或--ignore-zeros   忽略备份文件中的0 Byte区块，也就是EOF。
  -k或--keep-old-files   解开备份文件时，不覆盖已有的文件。
  -K<文件>或--starting-file=<文件>   从指定的文件开始还原。
  -l或--one-file-system   复制的文件或目录存放的文件系统，必须与tar指令执行时所处的文件系统相同，否则不予复制。
  -L<媒体容量>或-tape-length=<媒体容量>   设置存放每体的容量，单位以1024 Bytes计算。
  -m或--modification-time   还原文件时，不变更文件的更改时间。
  -M或--multi-volume   在建立，还原备份文件或列出其中的内容时，采用多卷册模式。
  -N<日期格式>或--newer=<日期时间>   只将较指定日期更新的文件保存到备份文件里。
  -o或--old-archive或--portability   将资料写入备份文件时使用V7格式。
  -O或--stdout   把从备份文件里还原的文件输出到标准输出设备。
  -p或--same-permissions   用原来的文件权限还原文件。
  -P或--absolute-names   文件名使用绝对名称，不移除文件名称前的"/"号。
  -r或--append   新增文件到已存在的备份文件的结尾部分。
  -R或--block-number   列出每个信息在备份文件中的区块编号。
  -s或--same-order   还原文件的顺序和备份文件内的存放顺序相同。
  -S或--sparse   倘若一个文件内含大量的连续0字节，则将此文件存成稀疏文件。
  -t或--list   列出备份文件的内容。
  -T<范本文件>或--files-from=<范本文件>   指定范本文件，其内含有一个或多个范本样式，让tar解开或建立符合设置条件的文件。
  -u或--update   仅置换较备份文件内的文件更新的文件。
  -U或--unlink-first   解开压缩文件还原文件之前，先解除文件的连接。
  -v或--verbose   显示指令执行过程。
  -V<卷册名称>或--label=<卷册名称>   建立使用指定的卷册名称的备份文件。
  -w或--interactive   遭遇问题时先询问用户。
  -W或--verify   写入备份文件后，确认文件正确无误。
  -x或--extract或--get  从备份文件中还原文件。
  -X<范本文件>或--exclude-from=<范本文件>  指定范本文件，其内含有一个或多个范本样式，让ar排除符合设置条件的文件。
  -z或--gzip或--ungzip   通过gzip指令处理备份文件。
  -Z或--compress或--uncompress   通过compress指令处理备份文件。
  -<设备编号><存储密度>   设置备份用的外围设备编号及存放数据的密度。
  --after-date=<日期时间>   此参数的效果和指定"-N"参数相同。
  --atime-preserve   不变更文件的存取时间。
  --backup=<备份方式>或--backup   移除文件前先进行备份。
  --checkpoint   读取备份文件时列出目录名称。
  --concatenate   此参数的效果和指定"-A"参数相同。
  --confirmation   此参数的效果和指定"-w"参数相同。
  --delete   从备份文件中删除指定的文件。
  --exclude=<范本样式>   排除符合范本样式的问家。
  --group=<群组名称>   把加入设备文件中的文件的所属群组设成指定的群组。
  --help   在线帮助。
  --ignore-failed-read   忽略数据读取错误，不中断程序的执行。
  --new-volume-script=<Script文件>   此参数的效果和指定"-F"参数相同。
  --newer-mtime   只保存更改过的文件。
  --no-recursion   不做递归处理，也就是指定目录下的所有文件及子目录不予处理。
  --null   从null设备读取文件名称。
  --numeric-owner   以用户识别码及群组识别码取代用户名称和群组名称。
  --owner=<用户名称>   把加入备份文件中的文件的拥有者设成指定的用户。
  --posix   将数据写入备份文件时使用POSIX格式。
  --preserve      此参数的效果和指定"-ps"参数相同。
  --preserve-order      此参数的效果和指定"-A"参数相同。
  --preserve-permissions      此参数的效果和指定"-p"参数相同。
  --record-size=<区块数目>      此参数的效果和指定"-b"参数相同。
  --recursive-unlink   解开压缩文件还原目录之前，先解除整个目录下所有文件的连接。
  --remove-files   文件加入备份文件后，就将其删除。
  --rsh-command=<执行指令>   设置要在远端主机上执行的指令，以取代rsh指令。
  --same-owner   尝试以相同的文件拥有者还原问家你。
  --suffix=<备份字尾字符串>   移除文件前先行备份。
  --totals   备份文件建立后，列出文件大小。
  --use-compress-program=<执行指令>   通过指定的指令处理备份文件。
  --version   显示版本信息。
  --volno-file=<编号文件>   使用指定文件内的编号取代预设的卷册编号。

### unzip

**功能说明：**解压缩zip文件

**语　　法：**unzip -cflptuvz-P <密码>文件[-x <文件>] 或 unzip [-Z]

**补充说明：**unzip为.zip压缩文件的解压缩程序。

**参　　数：**
  -c   将解压缩的结果显示到屏幕上，并对字符做适当的转换。
  -f   更新现有的文件。
  -l   显示压缩文件内所包含的文件。
  -p   与-c参数类似，会将解压缩的结果显示到屏幕上，但不会执行任何的转换。
  -t   检查压缩文件是否正确。
  -u   与-f参数类似，但是除了更新现有的文件外，也会将压缩文件中的其他文件解压缩到目录中。
  -v   执行是时显示详细的信息。
  -z   仅显示压缩文件的备注文字。
  -a   对文本文件进行必要的字符转换。
  -b   不要对文本文件进行字符转换。 
  -C   压缩文件中的文件名称区分大小写。
  -j   不处理压缩文件中原有的目录路径。
  -L   将压缩文件中的全部文件名改为小写。
  -M   将输出结果送到more程序处理。
  -n   解压缩时不要覆盖原有的文件。
  -o   不必先询问用户，unzip执行后覆盖原有文件。
  -P<密码>   使用zip的密码选项。
  -q   执行时不显示任何信息。
  -s   将文件名中的空白字符转换为底线字符。
  -V   保留VMS的文件版本信息。
  -X   解压缩时同时回存文件原来的UID/GID。
  [.zip文件]   指定.zip压缩文件。
  [文件]   指定要处理.zip压缩文件中的哪些文件。
  -d<目录>   指定文件解压缩后所要存储的目录。
  -x<文件>   指定不要处理.zip压缩文件中的哪些文件。
  -Z   unzip -Z等于执行zipinfo指令。



### zip

**功能说明：**压缩文件。
**语　　法：**zip -AcdDfFghjJKlLmoqrSTuvVwXyz$-kll-t <日k期时间>压缩文件-i <范本样式>
**补充说明：**zip是个使用广泛的压缩程序，文件经它压缩后会另外产生具有".zip"扩展名的压缩文件。
**参　　数：**
  -A   调整可执行的自动解压缩文件。
  -b<工作目录>   指定暂时存放文件的目录。
  -c   替每个被压缩的文件加上注释。
  -d   从压缩文件内删除指定的文件。
  -D   压缩文件内不建立目录名称。
  -f   此参数的效果和指定"-u"参数类似，但不仅更新既有文件，如果某些文件原本不存在于压缩文件内，使用本参数会一并将其加入压缩文件中。
  -F   尝试修复已损坏的压缩文件。
  -g   将文件压缩后附加在既有的压缩文件之后，而非另行建立新的压缩文件。
  -h   在线帮助。
  -i<范本样式>   只压缩符合条件的文件。
  -j   只保存文件名称及其内容，而不存放任何目录名称。
  -J   删除压缩文件前面不必要的数据。
  -k   使用MS-DOS兼容格式的文件名称。
  -l   压缩文件时，把LF字符置换成LF+CR字符。
  -ll   压缩文件时，把LF+CR字符置换成LF字符。
  -L   显示版权信息。
  -m   将文件压缩并加入压缩文件后，删除原始文件，即把文件移到压缩文件中。
  -n<字尾字符串>   不压缩具有特定字尾字符串的文件。
  -o   以压缩文件内拥有最新更改时间的文件为准，将压缩文件的更改时间设成和该文件相同。
  -q   不显示指令执行过程。
  -r   递归处理，将指定目录下的所有文件和子目录一并处理。
  -S   包含系统和隐藏文件。
  -t<日期时间>   把压缩文件的日期设成指定的日期。
  -T   检查备份文件内的每个文件是否正确无误。
  -u   更换较新的文件到压缩文件内。
  -v   显示指令执行过程或显示版本信息。
  -V   保存VMS操作系统的文件属性。
  -w   在文件名称里假如版本编号，本参数仅在VMS操作系统下有效。
  -x<范本样式>   压缩时排除符合条件的文件。
  -X   不保存额外的文件属性。
  -y   直接保存符号连接，而非该连接所指向的文件，本参数仅在UNIX之类的系统下有效。
  -z   替压缩文件加上注释。
  -$   保存第一个被压缩文件所在磁盘的卷册名称。
  -<压缩效率>   压缩效率是一个介于1-9的数值。