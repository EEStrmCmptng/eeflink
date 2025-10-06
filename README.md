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
This generates 200K records-per-second for 600 seconds or 10 minutes,
with 16 source, 16 mapper, and 16 sink tasks with DVFS policy
ondemand and running query1
```
```
cd ~/eeflink
MCFG="16;16;16" MQUERY="query1" FLINK_RATE="200000_600000" MPOLICY="ondemand" ./run_query1.sh dynamic
```

## Correct experiment output
```
numRecordsOutPerSecond_avg should match the benchmark
generating 200K records per second as we want
to minimize backpressure
```
```
                           name  numRecordsInPerSecond_avg  numRecordsOutPerSecond_avg  busyTime_%  backPressuredTime_%
        Operator_Latency Sink_0              200019.294444                    0.000000   11.216667                  0.0
        Operator_Latency Sink_1              200018.752778                    0.000000   12.183333                  0.0
       Operator_Latency Sink_10              200019.400000                    0.000000   11.400000                  0.0
       Operator_Latency Sink_11              200019.572222                    0.000000   10.866667                  0.0
       Operator_Latency Sink_12              200020.930556                    0.000000   11.216667                  0.0
       Operator_Latency Sink_13              200018.311111                    0.000000   12.083333                  0.0
       Operator_Latency Sink_14              200021.411111                    0.000000   11.083333                  0.0
       Operator_Latency Sink_15              200018.613889                    0.000000   11.350000                  0.0
        Operator_Latency Sink_2              200018.347222                    0.000000   12.083333                  0.0
        Operator_Latency Sink_3              200021.269444                    0.000000   11.233333                  0.0
        Operator_Latency Sink_4              200017.644444                    0.000000   11.500000                  0.0
        Operator_Latency Sink_5              200020.894444                    0.000000   10.666667                  0.0
        Operator_Latency Sink_6              200017.547222                    0.000000   11.033333                  0.0
        Operator_Latency Sink_7              200019.047222                    0.000000   10.600000                  0.0
        Operator_Latency Sink_8              200020.625000                    0.000000   10.883333                  0.0
        Operator_Latency Sink_9              200017.644444                    0.000000   12.300000                  0.0
              Operator_Mapper_0              200013.027778               200013.261111   48.016667                  0.0
              Operator_Mapper_1              200013.075000               200013.041667   49.800000                  0.0
             Operator_Mapper_10              200013.166667               200013.000000   50.816667                  0.0
             Operator_Mapper_11              200012.441667               200012.563889   50.816667                  0.0
             Operator_Mapper_12              200012.550000               200012.380556   49.466667                  0.0
             Operator_Mapper_13              200012.755556               200012.800000   50.600000                  0.0
             Operator_Mapper_14              200012.008333               200012.094444   52.416667                  0.0
             Operator_Mapper_15              200013.272222               200013.375000   53.666667                  0.0
              Operator_Mapper_2              200013.416667               200013.586111   51.066667                  0.0
              Operator_Mapper_3              200012.966667               200012.672222   51.583333                  0.0
              Operator_Mapper_4              200013.547222               200013.408333   51.133333                  0.0
              Operator_Mapper_5              200012.644444               200012.525000   51.533333                  0.0
              Operator_Mapper_6              200013.161111               200013.197222   52.133333                  0.0
              Operator_Mapper_7              200012.927778               200012.838889   50.550000                  0.0
              Operator_Mapper_8              200013.438889               200013.313889   50.700000                  0.0
              Operator_Mapper_9              200013.394444               200013.302778   52.183333                  0.0
 Operator_Source: Bids Source_0                   0.000000               200010.830556    0.000000                  0.0
 Operator_Source: Bids Source_1                   0.000000               200010.447222    0.000000                  0.0
Operator_Source: Bids Source_10                   0.000000               200010.605556    0.000000                  0.0
Operator_Source: Bids Source_11                   0.000000               200010.622222    0.000000                  0.0
Operator_Source: Bids Source_12                   0.000000               200010.597222    0.000000                  0.0
Operator_Source: Bids Source_13                   0.000000               200015.083333    0.000000                  0.0
Operator_Source: Bids Source_14                   0.000000               200010.630556    0.000000                  0.0
Operator_Source: Bids Source_15                   0.000000               200011.258333    0.000000                  0.0
 Operator_Source: Bids Source_2                   0.000000               200010.608333    0.000000                  0.0
 Operator_Source: Bids Source_3                   0.000000               200010.525000    0.000000                  0.0
 Operator_Source: Bids Source_4                   0.000000               200010.569444    0.000000                  0.0
 Operator_Source: Bids Source_5                   0.000000               200010.666667    0.000000                  0.0
 Operator_Source: Bids Source_6                   0.000000               200010.658333    0.000000                  0.0
 Operator_Source: Bids Source_7                   0.000000               200010.591667    0.000000                  0.0
 Operator_Source: Bids Source_8                   0.000000               200010.525000    0.000000                  0.0
 Operator_Source: Bids Source_9                   0.000000               200010.569444    0.000000                  0.0
```

