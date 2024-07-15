### README: Performance Measurement, Evaluation, and Analysis

## Prepare

1. **Ensure OpenJDK 8 is installed on the Linux server**:
   If OpenJDK 8 is not installed, run the following command:
   ```bash
   sudo apt update
   sudo apt install openjdk-8-jdk
   ```

2. **Install Alibaba, Bisheng, and Tencent-Kona JDKs**:
   - Locate the JDK packages in the `jdk8` directory and extract them:
   ```bash
   tar -xvf alibaba-jdk.tar.gz -C /path/to/jdk8/directory
   tar -xvf bisheng-jdk.tar.gz -C /path/to/jdk8/directory
   tar -xvf tencent-kona-jdk.tar.gz -C /path/to/jdk8/directory
   ```

3. **Verify JDK installation directories**:
   - Ensure the installation directories in `zheruan/PLAN/set_jdk.sh` are correct.

4. **Set up Flamegraph**:
   - Extract Flamegraph or clone it using git:
   ```bash
   git clone https://github.com/brendangregg/FlameGraph.git
   ```

## Assignment 1

For Assignment 1, you can run the following command to execute the SPECjvm2008 benchmarks:

```bash
java -jar SPECjvm2008.jar -ikv -i 2 \
    crypto \
    compiler.compiler \
    scimark.large
```

After running the benchmarks, check the result directory for the generated results.

## Assignment 2

For Assignment 2, run the provided script to execute the benchmarks:

```bash
/path/to/PLAN/2/run_benchmarks.sh
```

This will generate `perf.data` and the result files, which are necessary for Assignment 3.

## Assignment 3

### Analysis with `perf`

1. **Record performance data using `perf`**:
   - Run the `derby` benchmark with `perf` to collect detailed profiling data:
   ```bash
   perf record -a -g -o /path/to/perf.data java -jar SPECjvm2008.jar -ikv -i 3 derby
   ```

2. **Generate and analyze Flamegraphs**:
   - Use the FlameGraph tools to visualize the performance data:
   ```bash
   perf script > out.perf
   ./FlameGraph/stackcollapse-perf.pl out.perf > out.folded
   ./FlameGraph/flamegraph.pl out.folded > flamegraph.svg
   ```

   - Open `flamegraph.svg` in a web browser to identify performance bottlenecks.

3. **Detailed Analysis and Reporting**:
   - Compare the performance data from different JDKs (OpenJDK, Alibaba, Tencent, and Bisheng).
   - Identify hotspots and inefficiencies from the Flamegraphs.
   - Document the findings and provide optimization recommendations based on the analysis.

### Summary

By following the steps outlined in this README, you can set up the test environment, execute the benchmarks for Assignments 1 and 2, and perform detailed performance analysis using `perf` for Assignment 3. This comprehensive approach will help you measure, evaluate, and optimize the performance of different JDKs, providing valuable insights and actionable recommendations.
