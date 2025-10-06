# Energy Efficiency Flink Experiments

## Cloudlab Node Setup
### Assume 4 nodes with IP addresses 10.10.1.1, 10.10.1.2, 10.10.1.3, 10.10.1.4
```
10.10.1.1 -> JobManager
10.10.1.2 -> Source
10.10.1.3 -> Mapper
10.10.1.4 -> Sink
```

## 5 minutes
```
./prep-node.sh
```

## 15 minutes
```
git clone git@github.com:EEStrmCmptng/flink-simplified.git
cd flink-simplified/scripts
./makeflink.sh
```

## 3 mins
```
git clone git@github.com:EEStrmCmptng/flink-benchmarks.git
cd flink-benchmarks
mvn clean package
```


