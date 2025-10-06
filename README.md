# Energy Efficiency Flink Experiments

## Cloudlab Node Setup
### Assume 4 nodes with IP addresses 10.10.1.1, 10.10.1.2, 10.10.1.3, 10.10.1.4
```
10.10.1.1 -> JobManager
10.10.1.2 -> Source
10.10.1.3 -> Mapper
10.10.1.4 -> Sink
```
### Use one of the following node types: [c6220, c220g1, c220g2, c220g5]
![Example cloudlab node config](https://github.com/EEStrmCmptng/eeflink/blob/master/images/cloudlabnodes.png)

### Flink experiment setup:
![Example flink setup](https://github.com/EEStrmCmptng/eeflink/blob/master/images/flinksetup.png)


### Setup node: 5 minutes - Run on all four nodes
```
./prep-node.sh
```

### Build and install Flink: 15 minutes - Run on all four nodes
```
cd ~/eeflink
git clone git@github.com:EEStrmCmptng/flink-simplified.git
cd flink-simplified/scripts
./makeflink.sh
```

### Build and install benchmarks: 3 mins - Run on all four nodes
```
cd ~/eeflink
git clone git@github.com:EEStrmCmptng/flink-benchmarks.git
cd flink-benchmarks
mvn clean package
```

## Sample experimental run, run on JobManage node only
```
cd ~/eeflink
MCFG="16;16;16" FLINK_RATE="300000_600000" MPOLICY="ondemand" ./run_query1.sh dynamic
```

