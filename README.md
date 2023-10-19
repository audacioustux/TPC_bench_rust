# Monoio Benchmark

TCP ping-pong(not echo) is a common benchmark for network applications.

We will use 1K ping-pong to test performance of different runtimes. Server will receive 1K data(and parse it in real applications) and reply 1K data.

## Max throughput

With given connections(enough for fully utilize CPU cores which latency is not important), we can measure the maximum throughput.

## Fixed QPS

We can measure the latency and CPU utilization of different runtimes.

## How to run

Run diffrent servers:

```
./target/release/monoio-server --cores 1
./target/release/glommio-server --cores 1
taskset -c 1 ./target/release/tokio-server --cores 1

./target/release/monoio-server --cores 1 2 3 4
./target/release/glommio-server --cores 1 2 3 4
taskset -c 1-4 ./target/release/tokio-server --cores 1 2 3 4
```

Run client:

```
./target/release/client --target 10.0.0.0:40000 --cores 1 2 3 4 --conns-per-core 150
```

## Benchmark result

### new result

```bash
50.023: NAdd: 269962; NSum: 13960723; NAverage: 279084.188, LatencyAverage: 44.421 us # glommio
50.047: NAdd: 223087; NSum: 15166466; NAverage: 303044.188, LatencyAverage: 3946.339 us # monoio
50.009: NAdd: 284090; NSum: 14031236; NAverage: 280574.656, LatencyAverage: 4253.316 us # tokio
```

### old result

Full result is available in [中文版本](https://github.com/bytedance/monoio/blob/master/docs/zh/benchmark.md) / [English version](https://github.com/bytedance/monoio/blob/master/docs/zh/benchmark.md).
