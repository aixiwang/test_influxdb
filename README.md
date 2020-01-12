# test_influxdb
a simple tutorial to test influxdb

'''
1. install
Ubuntu & Debian (64-bit)

wget https://dl.influxdata.com/influxdb/releases/influxdb_0.13.0_amd64.deb
sudo dpkg -i influxdb_0.13.0_amd64.deb
MD5: bcca4c91bbd8e7f60e4a8325be67a08a

sudo service influxdb start


2. test influxdb by web UI
http://192.168.2.110:8083/


write data: TEST,host=shanghai T1=1,T2=2,T3=3

SELECT "host", "T1", "T2", "T3" FROM "TEST"
SELECT host, T1, T2, T3 FROM TEST


TEST
time    host    T1  T2  T3
2020-01-12T12:33:15.854812159Z      1   2   3
2020-01-12T12:35:29.019342017Z  "shanghai"  1   2   3


create db: CREATE DATABASE "db1"


3. test line protocol
http://192.168.2.110:8086

protocol defintion:
<measurement>[,<tag-key>=<tag-value>...] <field-key>=<field-value>[,<field2-key>=<field2-value>...] [unix-nano-timestamp]

example:
cpu,host=serverA,region=us_west value=0.64
payment,device=mobile,product=Notepad,method=credit billed=33,licenses=3i 1434067467100293230
stock,symbol=AAPL bid=127.46,ask=127.48
temperature,machine=unit42,type=assembly external=25,internal=37 1434067467000000000


please input command from console:

curl -i -XPOST "http://192.168.2.110:8086/write?db=_internal" --data-binary 'TEST,host=shanghai T1=1,T2=2,T3=3'

you will received:
HTTP/1.1 204 No Content
Request-Id: c0b45155-353c-11ea-8010-000000000000
X-Influxdb-Version: 0.13.0
Date: Sun, 12 Jan 2020 13:09:23 GMT


wget http://192.168.2.110:8086/query?q=SELECT+host%2C+T1%2C+T2%2C+T3+FROM+TEST&db=db1

'''
