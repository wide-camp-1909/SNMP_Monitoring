# Configuration
## SNMP Generator
snmp exporterを使用する時にsnmp.ymlが必要になる。  
snmp.ymlを素早く生成する方法を記載する。
### mibファイルをダウンロードする
```
cd snmp_exporter/generator/
git clone https://github.com/librenms/librenms.git
mv -r librenms/mibs/ mibs/
```
使用したいmibファイルをmibs配下に移動する．  
例：arubaosの場合
```
cd /mibs
mv arubaos/* ./
```

### generator.ymlを作成する
参考サイト：https://hakengineer.xyz/2018/05/20/post-1214/#generatoryml

### snmp.ymlを作成する
```
cd ../
docker build -t snmp-generator .
docker run -ti \
-v $PWD/mibs/:/root/.snmp/mibs \
-v $PWD/generator.yml:/opt/generator.yml:ro \
-v $PWD/out/:/opt/ \
--rm snmp-generator generate
```