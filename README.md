# criu-ol
Using CRIU to test OpenLiberty based applications

## Prerequisites
* Install CRIU:
   - On ubuntu `sudo apt install criu`
   - On rhel `sudo yum install criu`
* Download [OpenLiberty](https://public.dhe.ibm.com/ibmdl/export/pub/software/openliberty/runtime/release/2019-11-20_0300/openliberty-19.0.0.12.zip)
* Clone this repository

## Configure and run the applications:
In the following steps it is assumed that this repository is cloned at `/opt/criu-ol`.

Please change the location according to your setup.

Make sure following steps are run as `root` user.

### pingperf
   - create a directory where the app would be placed:
     ```
     # mkdir /opt/app/pingperf
     # cd /opt/app/pingperf
     ```
   - extract the downloaded openliberty zip here:
     `# unzip -q <path to openliberty zip>`
   - create server
     `# ./wlp/bin/server create defaultServer`
   - copy app files from the cloned repo to /opt/criu-test/pingperf/
     ```
     # cp /opt/criu-ol/pingperf/pingperf.war ./wlp/usr/servers/defaultServer/apps
     # cp /opt/criu-ol/pingperf/jvm.options ./wlp/usr/servers/defaultServer
     # cp /opt/criu-ol/pingperf/server.xml ./wlp/usr/servers/defaultServer
     ```
   - Go to top directory of the cloned repo:
     `# cd /opt/criu-ol`
   - Adjust the variables in `pingperf_test.sh` according to the app location and run the script as:
   
     `# ./pingperf_test.sh <batches> <iterations>`
     
     eg `# ./pingperf_test.sh 5 8` would run 5 batches with 8 iterations in each batch.

     If all goes fine, a summary would be displayed at the end of the run.
     
### acmeair
   - create a directory where the app would be placed:
     ```
     # mkdir /opt/app/acmeair
     # cd /opt/app/acmeair
     ```
   - extract the downloaded openliberty zip here:
     `# unzip -q <path to openliberty zip>`
   - create server
     `# ./wlp/bin/server create defaultServer`
   - copy app files from the cloned repo to /opt/criu-test/acmeair/
     ```
     # cp /opt/criu-ol/acmeair/acmeair-webapp-2.0.0-SNAPSHOT.war ./wlp/usr/servers/defaultServer/apps
     # cp /opt/criu-ol/acmeair/mongo.properties ./wlp/usr/servers/defaultServer
     # cp /opt/criu-ol/acmeair/server.xml ./wlp/usr/servers/defaultServer
     ```
   - create mongdb docker image using the script in the cloned repo
     ```
     # /opt/criu-test/acmeair
     # ./build_mongo.sh
     ```
   - Go to top directory of the cloned repo:
     `# cd /opt/criu-ol`
   - Adjust the variables in `acmear_test.sh` according to the app location and run the script as:

     `# ./acmeair_test.sh <batches> <iterations>`

     eg: `# ./acmeair_test.sh 5 8` would run 5 batches with 8 iterations in each batch.

     If all goes fine, summary would be displayed at the end of the run.

### daytrader7
   - create a directory where the app would be placed:
     ```
     # mkdir /opt/app/daytrader7
     # cd /opt/app/daytrader7
     ```
   - extract the downloaded openliberty zip here:
     `# unzip -q <path to openliberty zip>`
   - create server
     `# ./wlp/bin/server create defaultServer`
   - copy app files from the cloned repo to /opt/criu-test/acmeair/
     ```
     # cp /opt/criu-ol/daytrader7/shared ./wlp/usr/
     # cp /opt/criu-ol/daytrader7/servers/defaultServer ./wlp/usr/servers
     ```
   - Go to top directory of the cloned repo:
     `# cd /opt/criu-ol`
   - Adjust the variables in `daytrader7_test.sh` according to the app location and run the script as:
   
     `# ./daytrader7_test.sh <batches> <iterations>`
     
     eg `# ./daytrader7_test.sh 5 8` would run 5 batches with 8 iterations in each batch.

     If all goes fine, a summary would be displayed at the end of the run.     
