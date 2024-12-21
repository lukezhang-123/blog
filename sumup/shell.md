
# tcpdump
tcpdump -i any port 3306 and host 10.1.1.1 -s 65535 -X -q -tttt -nn -C 100m -W 50 -w /tmp/mysql.pcap

tcpdump dst port 3066

# 找到Unix行，替换下一行
sed '/Unix/{n;s/.*/hi/}' file
