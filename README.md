# open62541-nodeset-exporter-demo

## General

A C++ 20 and CMake demo project showing how to use the nodesetexporter and open62541 libraries pre-installed on the
system
as shared libraries in your project.

This version is used for nodesetexporter 1.1.0 and above.\
For nodesetexporter version 1.0.0, use demo version v1.0.0.

## Dependencies

OS: Linux (Debian, Ubuntu, ...)

To build you will need installed in your system:

- git
- make
- cmake
- GCC (C++20 features are available since GCC 8, but development was carried out on GCC 12).
  https://gcc.gnu.org/projects/cxx-status.html
- pre-compiled and pre-installed open62541 version 1.3.x or 1.4.x
- pre-compiled and pre-installed nodesetexporter

Note: One of the nodesetexporter library header files uses ftm. It can be installed in various ways. In this case, it is
used as included code in the project in the 3rdparty folder.

## How to build

In the shell you need to run the following commands::

```bash
git clone https://github.com/xydan83/open62541-nodeset-exporter-demo.git
cd open62541-nodeset-exporter-demo/
mkdir build
cd build
cmake ..
make -j
```

(!) **As a rule, the master branch may differ from the release versions, so do not forget to switch using
`git checkout tags/v1.x.x` after `cd open62541-nodeset-exporter-demo/`.**


After this, an executable file `nodesetexporter-demo` will be created. You can execute the demo to
export OPC UA nodeset from any starting node.
You can try using the OPC UA demo server: `opc.tcp://opcua.demo-this.com:51210/UA/SampleServer` and "start
node" `ns=4;i=1240`.
Link to the server from here: https://kb.opclabs.com/OPC_UA_Demo_Servers.

To run the executable,
do: `./nodesetexporter-demo opc.tcp://opcua.demo-this.com:51210/UA/SampleServer "ns=4;i=1240"`.
The first parameter is the address of the OPC UA server, the second is the starting node.
After browsing and exporting you will see a file `demo_export.xml` with a nodeset.

## More info

For the open62541 OPC UA library, see here: https://github.com/open62541/open62541

For the nodesetexporter library, see here: https://github.com/xydan83/open62541-nodeset-exporter

## License

MPL2.0: https://github.com/xydan83/open62541-nodeset-exporter-insource-demo/blob/main/LICENSE